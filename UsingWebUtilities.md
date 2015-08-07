
# Introduction #

**webutilities** provides Set of classes implemented as J2EE components ([Servlet](#JSCSSMergeServlet.md), [Filter](#YUIMinFilter.md) and [CustomTag](#YuiMinTag.md)) to help you speed up your front end performance. These components can be used to do some JS,CSS optimizations in running webapp like grouping multiple resources in one call or compressing them on the fly using YUI compressor.

Currently it has following components which can use easily used in J2EE webapp.

  * **[JSCSSMergeServlet](#JSCSSMergeServlet.md)** - to merge multiple JS or CSS and serve them in one HTTP request.
  * **[YUIMinFilter](#YUIMinFilter.md)** - to compress JS or CSS resources on the fly using YUI compressor.
  * **[YuiMinTag](#YuiMinTag.md)** - Custom tag to compress inline JS and CSS code using YUI compressor in JSPs.

More details and usage of each one is mentioned below. If you facing any issues, please feel free to report [here](http://code.google.com/p/webutilities/issues/entry).

# Merge multiple JS or CSS file in one HTTP request #
## `JSCSSMergeServlet` ##

## Details ##

Using **`JSCSSMergeServlet`** the multiple JS or CSS resources can be grouped together (by adding comma) in one HTTP call. It also has an option to add appropriate expires header to take advantage of browser caching.

## Usage ##

Put the **[webutilities-x.y.z.jar](http://code.google.com/p/webutilities/downloads/detail?name=webutilities-0.0.2.jar&can=2&q=)** in your classpath (WEB-INF/lib folder of your webapp).

Declare this servlet in your **`web.xml`** ( web descriptor file)

```
 <servlet>
 	<servlet-name>JSCSSMergeServlet</servlet-name>
 	<servlet-class>com.googlecode.webutilities.servlets.JSCSSMergeServlet</servlet-class>
 	<!-- This init param is optional and default value is minutes for 7 days in future. To expire in the past use negative value. --> 
 	<init-param>
		<param-name>expiresMinutes</param-name>
		<param-value>7200</param-value> <!-- 5 days -->
 	</init-param>
	<!-- This init param is also optional and default value is true. Set it false to override.-->
        <init-param>
		<param-name>useCache</param-name>
		<param-value>false</param-value> 
 	</init-param>
 </servlet>
```

Map this servlet to serve your JS and CSS resources
```
 <servlet-mapping>
   <servlet-name>JSCSSMergeServlet</servlet-name>
   <url-pattern>*.js</url-pattern>
   <url-pattern>*.json</url-pattern>
   <url-pattern>*.css</url-pattern>
 </servlet-mapping>
```

In your web pages (HTML or JSP files) combine your multiple JS or CSS in one request as shown below.

To serve multiple JS files through one HTTP request
```
 <script language="JavaScript" src="/myapp/js/prototype,controls,dragdrop,myapp.js"></script>
```

To serve multiple CSS files through one HTTP request
```
 <link rel="StyleSheet" href="/myapp/css/common,calendar,aquaskin.css"/>
```

Also if you wanted to serve them minified all together then you can add **`YUIMinFilter`** on them. See `YUIMinFilter`  for details.

## Init Parameters ##
Both init parameters are optional.

**expiresMinutes** has default value of 7 days. This value is relative from current time. Use negative value to expire early in the past. Ideally you should never be using negative value otherwise you won't be able to take advantage of browser caching for static resources.

  * **expiresMinutes** - Relative number of minutes (added to current time) to be set as Expires header
  * **useCache** - to cache the earlier merged contents and serve from cache. Default true.

## Dependencies ##

  * **servlet-api.jar** - Must be already present in your webapp classpath

## Notes on Cache ##

If you have not set **useCache** init parameter to false then cache will be used and contents will be always served from cache if found. Sometimes you may not want to use cache or you may want to evict the cache then using URL parameters you can do that.

### URL Parameters to skip or evict the cache ###

  * **`_skipcache_`** - The JS or CSS request URL if contains this parameters the cache will not be used for it.
  * **`_dbg_`**- same as above _skipcache_ parameter.
  * **`_expirecache_`** - The cache will be cleaned completely. All existing cached contents will be cleaned.

> Eg.
```
 <link rel="StyleSheet" href="/myapp/css/common,calendar,aquaskin.css?_dbg_=1"/>
```
> or
```
 <script language="JavaScript" src="/myapp/js/prototype,controls,dragdrop,myapp.js?_expirecache_=1"></script>
```

## Limitations ##
The multiple JS or CSS files can be combined together in one request if they are in same parent path. eg. /myapp/js/a.js, /myapp/js/b.js and /myapp/js/c.js can be combined together as /myapp/js/a,b,c.js. If they are not in common path then they can not be combined in one request. Same applies for CSS too.

# Minify/Compress external JS and CSS files on the fly using YUI Compressor #
## `YUIMinFilter` ##

## Details ##

The **`YUIMinFilter`** is implemented as Servlet Filter to enable on the fly minification of JS and CSS resources using YUICompressor. Using the YUIMinFilter the JS and CSS resources can be minified in realtime by adding this filter.

## Usage ##

Put the **[webutilities-x.y.z.jar](http://code.google.com/p/webutilities/downloads/detail?name=webutilities-0.0.2.jar&can=2&q=)** and **[yuicompressor-x.y.z.jar](http://yuilibrary.com/downloads/#yuicompressor)** (See dependency mentioned below) in your classpath (WEB-INF/lib folder of your webapp).

Declare this Filter in your **`web.xml`** ( web descriptor file)

```
 <filter>
 	<filter-name>yuiMinFilter</filter-name>
 	<filter-class>com.googlecode.webutilities.yuimin.YUIMinFilter</filter-class>
 	<!-- All the init params are optional and are equivalent to YUICompressor command line options --> 
 	<init-param>
		<param-name>lineBreak</param-name>
		<param-value>8000</param-value>
 	</init-param>
 </filter>
```

Map this filter on your JS and CSS resources

```
 <filter-mapping>
   <filter-name>yuiMinFilter</filter-name>
   <url-pattern>*.js</url-pattern>
   <url-pattern>*.json</url-pattern>
   <url-pattern>*.css</url-pattern>
 </filter-mapping>
```

And you are all done! All your JS and CSS files should get minified on the fly.

## Init Parameters ##

All the init parameters are optional and are as explained below.

  * **lineBreak** - equivalent to YUICompressor --line-break. Insert a line break after the specified column number
  * **noMunge** - equivalent to YUICompressor --nomunge. Minify only, do not obfuscate. Default false.
  * **preserveSemi** - equivalent to YUICompressor --preserve-semi. Preserve all semicolons. Default false.
  * **disableOptimizations** - equivalent to YUICompressor --disable-optimizations. Disable all micro optimizations. Default false.
  * **useCache** - to cache the earlier minified contents and serve from cache. Default true.

## Dependencies ##

The `YUIMinFilter` depends on servlet-api and YUICompressor jar to be in the classpath.

  * **servlet-api.jar** - Must be already present in your webapp classpath
  * **[yuicompressor-x.y.z.jar](http://yuilibrary.com/downloads/#yuicompressor)** - Download and put appropriate version of this jar in your classpath (in WEB-INF/lib)

## Notes on Cache ##

If you have not set **useCache** init parameter to false then cache will be used and contents will be always served from cache if found. Sometimes you may not want to use cache or you may want to evict the cache then using URL parameters you can do that.

### URL Parameters to skip or evict the cache ###

  * **`_skipcache_`** - The JS or CSS request URL if contains this parameters the cache will not be used for it.
  * **`_dbg_`**- same as above _skipcache_ parameter.
  * **`_expirecache_`** - The cache will be cleaned completely. All existing cached contents will be cleaned.

> Eg.
```
 <link rel="StyleSheet" href="/myapp/css/common.css?_dbg_=1"/>
```
> or
```
 <script language="JavaScript" src="/myapp/js/prototype.js?_expirecache_=1"></script>
```

## Limitations ##

Current version of `YUIMinFilter` **does not support charset option**.

As a best practice you should also add appropriate expires header on static resources so that browser caches them and doesn't request them again and again. You can use the `JSCSSMergeServlet` to add expires header on JS and CSS. It also helps combines multiple JS or CSS requests in one HTTP request. See JSCSSMergeServlet for details.

# Compress inline JS or CSS code using YUI Compressor #
## `YuiMinTag` ##

## Details ##

The **`YuiMinTag`** is the JSP custom tag to expose the YUICompressor functionality in the JSP. Using the YuiMinTag inline CSS, JS can be compressed.

## Usage ##

Put the **[webutilities-x.y.z.jar](http://code.google.com/p/webutilities/downloads/detail?name=webutilities-0.0.2.jar&can=2&q=)** and [yuicompressor-x.y.z.jar](http://yuilibrary.com/downloads/#yuicompressor)**(See dependency mentioned below) in your classpath (WEB-INF/lib folder of your webapp).**

Delcare the taglib and prefix in your JSP file

```
<%@ taglib uri="http://webutilities.googlecode.com/taglib/yuimin" prefix="ymin" %>
```

Use the tag to minify your inline JavaScript

```
 <ymin:minify type="js">
        //...
  	// your inline uncompressed JS
  	//... 	
 </ymin:minify>
```

You can also similarly use the tag to minify your inline style
```
 <ymin:minify type="css">
  	//...
  	// your inline uncompressed CSS
  	//...
 </ymin:minify>
```

## Attributes ##

The `YuiMinTag` also supports the different attributes similar to YUICompressor's command line options. Below are the attributes and their explanations. all attrinutes are optional except **type**.

  * **type** - possible values are js or css. The only required attribute. Usage as seen above.
  * **lineBreak** - equivalent to YUICompressor --line-break. Insert a line break after the specified column number
  * **noMunge** - equivalent to YUICompressor --nomunge. Minify only, do not obfuscate. Default false.
  * **preserveSemi** - equivalent to YUICompressor --preserve-semi. Preserve all semicolons. Default false.
  * **disableOptimizations** - equivalent to YUICompressor --disable-optimizations. Disable all micro optimizations. Default false.

## Dependencies ##

The `YuiMinTag` depends on jsp-api and YUICompressor jar to be in the classpath.

  * **jsp-api.jar** - Must be already present in your webapp classpath
  * **[yuicompressor-x.y.z.jar](http://yuilibrary.com/downloads/#yuicompressor)** - Download and put appropriate version of this jar in your classpath (in WEB-INF/lib)

## Limitations ##

Current version of `YuiMinTag` **does not support charset option**.
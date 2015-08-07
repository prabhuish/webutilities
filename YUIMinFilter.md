Minification removes unwanted characters to reduce the size. This is one of the performance improvement technique (http://developer.yahoo.com/performance/rules.html#minify). [YUICompressor](http://developer.yahoo.com/yui/compressor/) is the minification tool from Yahoo!.

**[YUIMinFilter](YUIMinFilter.md)** is implemented as Servlet Filter to enable on the fly minification of JS and CSS resources using [YUICompressor](http://developer.yahoo.com/yui/compressor/) internally. JS and CSS resources can be minified runtime by adding this filter. It is also advised to use ResponseCacheFilter so that result of this minification will be cached and served from cache next time for even faster loading.


# Configuration #

Declare this Filter in your **`web.xml`** ( web descriptor file)

```
 <filter>
 	<filter-name>yuiMinFilter</filter-name>
 	<filter-class>com.googlecode.webutilities.filters.YUIMinFilter</filter-class>
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

# Usage #
Once it is configured on js, css extensions, it served those resources minified on the fly when requested. There is no anything else needed. If you have also configured merge servlet then those multiple merged JS or CSS will also be minified on the fly using this.

# Customization #

All the init parameters are optional and are as explained below.

  * **lineBreak** - equivalent to YUICompressor --line-break. Insert a line break after the specified column number
  * **noMunge** - equivalent to YUICompressor --nomunge. Minify only, do not obfuscate. Default false.
  * **preserveSemi** - equivalent to YUICompressor --preserve-semi. Preserve all semicolons. Default false.
  * **disableOptimizations** - equivalent to YUICompressor --disable-optimizations. Disable all micro optimizations. Default false.
  * **charset** - equivalent to YUICompressor --charset. Charset to be used. Default UTF-8.

Besides above parameters, each filter has [these  common init parameters](CommonFilterParameters.md) to better customize and configure it.
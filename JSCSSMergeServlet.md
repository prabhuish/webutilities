Server calls are costly. Each new HTTP request has overhead of DNS lookup, request initialization, making actual request to get the data. For better performance it is [advised to make Fewer HTTP requests](http://developer.yahoo.com/performance/rules.html#num_http). This can be done by [Combining multiple JS](http://code.google.com/speed/page-speed/docs/rtt.html#CombineExternalJS) or [Combining multiple CSS files](http://code.google.com/speed/page-speed/docs/rtt.html#CombineExternalCSS) into few. We can reduce HTTP requests if we combine required multiple static resources together and get them in one request.

**[JSCSSMergeServlet](JSCSSMergeServlet.md)** groups and merge multiple JS or CSS files in a single HTTP call. There is no need to merge them manually or save in a single file. You just need to request them using single URL and put multiple resources separated by comma as shown below. _This servlet can also be used to [Add appropriate Expires/Cache-Control headers](AddExpiresHeader.md) for images, JS or CSS files._


# Configuration #

Declare this servlet in your **`web.xml`** ( web descriptor file)

```
 <servlet>
 	<servlet-name>JSCSSMergeServlet</servlet-name>
 	<servlet-class>com.googlecode.webutilities.servlets.JSCSSMergeServlet</servlet-class>
 	<!-- This init param is optional and default value is minutes for 7 days in future. --> 
 	<init-param>
		<param-name>expiresMinutes</param-name>
		<param-value>14400</param-value> <!-- 10 days -->
 	</init-param>
	<!-- This init param is also optional and default value is 'public'.-->
        <init-param>
		<param-name>cacheControl</param-name>
		<param-value>public</param-value> 
 	</init-param>
 </servlet>
```

Map this servlet to serve your JS and CSS resources. You can also map this servlet on images (`*.png, *.gif` etc.) it will not merge them but will add Expires/Cache-Control headers only.
```
 <servlet-mapping>
   <servlet-name>JSCSSMergeServlet</servlet-name>
   <url-pattern>*.js</url-pattern>
   <url-pattern>*.json</url-pattern>
   <url-pattern>*.css</url-pattern>
 </servlet-mapping>
```

# Usage #

In your web pages (HTML or JSP files) combine your multiple JS or CSS in one request as shown below.

To serve multiple JS files (from same or different folder on server) through one HTTP request. Only last resource should end with appropriate extension.
```
 <!-- To Serve following four JS files in one request

  1. /appContext/js/libs/prototype.js
  2. /appContext/js/controls/controls.js 
  3. /appContext/js/controls/dragdrop.js 
  4. /appContext/js/utils/util.js    -->

 <script language="JavaScript" src="/appContext/js/libs/prototype,../controls/controls,dragdrop,../utils/util.js"></script>
<!-- You can specify absolute or relative path for each resource. Relative path is always relative to the previous resource. -->
```

To serve multiple CSS files through one HTTP request

```
  <!-- To Serve following 3 CSS files in one request

  1. /appContext/css/common.css
  2. /appContext/css/aqua/calendar.css
  3. /appContext/css/aqua/skin.css   -->

 <link rel="StyleSheet" href="/appContext/css/common,/css/aqua/calendar,skin.css"/>
```

Also if you wanted to serve them minified all together then you can also add **YUIMinFilter**. It is also advised that you configure **ResponseCacheFilter** so that the result of this merging will be cached to speed up further requests by avoiding reading, merging them again next time.

# URLs in CSS #

Because of such merging of CSS files, the relative URLs used for images in CSS are likely to be wrong. This servlets takes care of replacing relative URLs to their respective absolute path.

For Example. If  above calendar.css, which is inside /css/aqua folder has following rule.

```
...
.CalendarTitle{
    ...
    background-image: url(images/title.png);  
    ...
}
```

It means that there is /css/aqua/images folder and title.png is inside that. But because of above merged request, this reference will be wrong ("/appContext/css/common,/css/aqua/images/title.png").

This servlet will correct it to proper absolute path and will serve it as shown below.

```
...
.CalendarTitle{
    ...
    background-image: url(/appContext/css/aqua/images/title.png);  
    ...
}
```

This behavior is controlled using init parameter **autoCorrectUrlsInCSS**

# Customization #

  * **expiresMinutes** - Set expired header. Relative number of minutes (added to current time). Default 10080.
  * **cacheControl** - set Cache-Control header. Default value "public".
  * **autoCorrectUrlsInCSS** - whether to correct relative URLs in CSS and make them absolute. Default true.

Above first two parameters are used to enable client side caching. For more details please look at [Adding Expires/Cache-Control header](AddExpiresHeader.md) section.
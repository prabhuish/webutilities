We can [Leverage Browser Caching](http://code.google.com/speed/page-speed/docs/caching.html#LeverageBrowserCaching) at client side by adding appropriate response headers. Static contents like JS, CSS, images etc. are less frequently changing resources. That means once sent to the browser, it is safe for browser to cache them locally and use from there instead of requesting again from the server. This is done by setting enough future dated value in Expires header of the response. This value tells browser about how much time to store this response contents in a cache. Such resources need to have expired header value adequate far in future (more 7 days or a month) or as never expires (more than a year).

Using Same **[JSCSSMergeServlet](JSCSSMergeServlet.md)** we can specify the Expires header, Cache-Control header values to JS, CSS resources and also images. Although we won't be requesting multiple image files using this Servlet but for images we can use it to add appropriate headers only.



# Configuration #
Same like what we did for [Minimize HTTP Requests](MinimizeHTTPRequests.md). If you have already declared it to merge the CSS/JS files then you need not to declare it again. You can reuse the same one for adding expires header to JS/CSS and Image files. You can add define url-patten in mappings to include JS/CSS and Images.

Declare this servlet in your **`web.xml`** ( web descriptor file)
```
 <servlet>
 	<servlet-name>JSCSSMergeServlet</servlet-name>
 	<servlet-class>com.googlecode.webutilities.servlets.JSCSSMergeServlet</servlet-class>
 	<!-- This init param is optional and default value is minutes for 7 days in future. --> 
 	<init-param>
		<param-name>expiresMinutes</param-name>
		<param-value>43200</param-value> <!-- for 30 days -->
 	</init-param>
	<!-- This init param is also optional and default value is "public".-->
        <init-param>
		<param-name>cacheControl</param-name>
		<param-value>public</param-value> 
 	</init-param>
 </servlet>
```

Map this servlet to serve your JS,CSS and images.
```
 <servlet-mapping>
   <servlet-name>JSCSSMergeServlet</servlet-name>
   <url-pattern>*.js</url-pattern>
   <url-pattern>*.json</url-pattern>
   <url-pattern>*.css</url-pattern>
   <url-pattern>*.png</url-pattern>
   <url-pattern>*.jpg</url-pattern>
   <url-pattern>*.gif</url-pattern>
 </servlet-mapping>
```

# Usage #

As a result of this, all your JS, CSS and Images file being requested will have appropriate Expires header added to them with specified value. You don't need anything extra. Any files with matching extension as configured (in url-patterns) will automatically have proper headers as specified. Below examples are just for demonstration.

Requesting single JS file. Response of this will have appropriate Expires header.
```
<script language="JavaScript" src="/appContext/js/libs/prototype.js"></script>
```

Same will work for merged resources request.
```
<script language="JavaScript" src="/appContext/js/libs/prototype,scriptaculous,controls.js"></script>
```

Similarly for CSS (single or merged) request.

Even images being requested either from CSS or HTML will have appropriate Expires header.

```
<img src="/images/logo.png">
```
```
<style>
   #logo {
      background:url("/images/logo.png") no-repeat;
   }
</style>
```

# Customization #

Both these init parameters are optional with standard default values.

  * **expiresMinutes** - Relative number of minutes (added to current time) to be set as Expires header. Default 10080 (7 days).
  * **cacheControl** - set Cache-Control header. Default value "public".
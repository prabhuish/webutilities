When you are configuring multiple filters and servlet on similar resources (urls), the response generation will chain through each one by one as per the order in which it is configured.

The Recommended order is...
  1. [JSCSSMergeServlet](JSCSSMergeServlet.md)
```
 <!-- Declaration -->
 <servlet>
        <servlet-name>JSCSSMergeServet</servlet-name>
        <servlet-class>com.googlecode.webutilities.servlets.JSCSSMergeServlet</servlet-class>
        <init-param>
                <param-name>expiresMinutes</param-name>
                <param-value>43200</param-value> <!-- 30 days -->
        </init-param>
 </servlet>
 <!-- Mapping -->
 <servlet-mapping>
  <servlet-name>JSCSSMergeServet</servlet-name>
   <url-pattern>*.js</url-pattern>
   <url-pattern>*.json</url-pattern>
   <url-pattern>*.css</url-pattern>
   <url-pattern>*.png</url-pattern>
   <url-pattern>*.jpg</url-pattern>
   <url-pattern>*.gif</url-pattern>
 </servlet-mapping>

```
  1. [CharacterEncodingFilter](CharacterEncodingFilter.md)
```
 <!-- Declaration -->
 <filter>
        <filter-name>charEncodingFilter</filter-name>
        <filter-class>com.googlecode.webutilities.filters.CharacterEncodingFilter</filter-class>
        <init-param>
        	<param-name>encoding</param-name>
   			<param-value>UTF-8</param-value>
   		</init-param>
   		<init-param>
        	<param-name>force</param-name>
   			<param-value>true</param-value>
   		</init-param>
   		<init-param>
        	<param-name>ignoreURLPattern</param-name>
   			<param-value>.*\.(png|gif|jpg|tiff|bmp|mpg|jpeg)</param-value>
   		</init-param>
 </filter>
 <!-- Mapping -->
  <filter-mapping>
   <filter-name>charEncodingFilter</filter-name>
   <url-pattern>/*</url-pattern>
 </filter-mapping>

```
  1. [ResponseCacheFilter](ResponseCacheFilter.md)
```
 <!-- Declaration -->
 <filter>
        <filter-name>responseCacheFilter</filter-name>
        <filter-class>com.googlecode.webutilities.filters.ResponseCacheFilter</filter-class>
 </filter>
 <!-- Mapping -->
 <filter-mapping>
   <filter-name>responseCacheFilter</filter-name>
   <url-pattern>*.js</url-pattern>
   <url-pattern>*.json</url-pattern>
   <url-pattern>*.css</url-pattern>
 </filter-mapping>

```
  1. [CompressionFilter](CompressionFilter.md)
```
<!-- Declaration -->
  <filter>
        <filter-name>compressionFilter</filter-name>
        <filter-class>com.googlecode.webutilities.filters.CompressionFilter</filter-class>
        <init-param>
                <param-name>compressionThreshold</param-name>
                <param-value>512</param-value> <!--  anything above 512bytes  -->
        </init-param>
        <init-param>
        	<param-name>ignoreURLPattern</param-name>
   		<param-value>.*\.(png|gif|jpg|tiff|bmp|mpg|jpeg)</param-value>
   	</init-param>	
 </filter>
 <!-- Mapping -->
 <filter-mapping>
   <filter-name>compressionFilter</filter-name>
   <url-pattern>/*</url-pattern>
 </filter-mapping>

```
  1. [YUIMinFilter](YUIMinFilter.md)
```
 <!-- Declaration -->
 <filter>
        <filter-name>yuiMinFilter</filter-name>
        <filter-class>com.googlecode.webutilities.filters.YUIMinFilter</filter-class>
 </filter>
 <!-- Mapping -->
  <filter-mapping>
  <filter-name>yuiMinFilter</filter-name>
  <url-pattern>*.js</url-pattern>
  <url-pattern>*.json</url-pattern>
  <url-pattern>*.css</url-pattern>

 </filter-mapping>

```

[Specifying a character set early](http://code.google.com/speed/page-speed/docs/rendering.html#SpecifyCharsetEarly) for your HTML documents allows the browser to begin executing scripts immediately.

**`CharacterEncodingFilter`** can be used to set character encoding to the request if not already set. It also has an option to enforce the specified encoding irrespective of what is set by the page. Useful when you want to force certain character encoding across the pages. Also note that do not wrongly set charset on binary resources such images, videos etc.


# Configuration #

Declare this filter in your web.xml (web descriptor file).

```
 <filter>
        <filter-name>characterEncodingFilter</filter-name>
        <filter-class>com.googlecode.webutilities.filters.CharacterEncodingFilter</filter-class>
        <!-- init params  -->
        <init-param>
                <param-name>encoding</param-name>
                <param-value>UTF-8</param-value>
        </init-param>
        <init-param>
                <param-name>force</param-name>
                <param-value>true</param-value> <!-- true if you wanted to force encoding  -->
        </init-param>
        <init-param>
                <param-name>ignoreURLPattern</param-name>
                <param-value>.*\.(png|jpg|gif)|.*/image?/.*</param-value> <!-- regular expression to be matched against URL to skip setting encoding on -->
        </init-param>
 </filter>
```

Map this filter on your web requests

```
 <filter-mapping>
   <filter-name>characterEncodingFilter</filter-name>
   <url-pattern>*</url-pattern>
 </filter-mapping>
```

# Usage #

Since it is Filter, you don't need anything extra to use it. Once configured and mapped as above on specified URL pattern, the filter will do it's job to apply said encoding as appropriate.

# Customization #

You can customize it using init parameters. All the init parameters are optional and explained below.

  * **encoding** - name of the encoding that you wanted to set. e.g. UTF-8
  * **force** - true or false. If true this encoding will be forced and overwrite already set encoding for both request and response.

Besides above parameters, each filter has [these  common init parameters](CommonFilterParameters.md) to better customize and configure it.
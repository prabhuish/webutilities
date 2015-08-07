All the filters accept following common init parameters.

# Configuration #

Declare this filter in your web.xml (web descriptor file).

```
 <filter>
        <filter-name>X</filter-name>
        <filter-class>X</filter-class>
        <!-- init params  -->
        <init-param>
                <param-name>acceptURLPattern</param-name>
                <param-value>.*</param-value> <!-- regex -->
        </init-param>
        <init-param>
                <param-name>ignoreURLPattern</param-name>
                <param-value>.*\.(png|jpg|gif)|.*/image?/.*</param-value> <!-- regular expression to be matched against URL to skip setting encoding on -->
        </init-param>
        <init-param>
                <param-name>acceptQueryStringPattern</param-name>
                <param-value>.*</param-value> <!-- regex -->
        </init-param>
        <init-param>
                <param-name>ignoreQueryStringPattern</param-name>
                <param-value>__DBG__=1</param-value>
        </init-param>
        <init-param>
                <param-name>acceptMIMEPattern</param-name>
                <param-value>.*</param-value> <!-- regex -->
        </init-param>
        <init-param>
                <param-name>ignoreMIMEPattern</param-name>
                <param-value>image/gif</param-value> 
        </init-param>
        <init-param>
                <param-name>ignoreUAPattern</param-name>
                <param-value>.*</param-value> <!-- regex -->
        </init-param>
        <init-param>
                <param-name>ignoreUAPattern</param-name>
                <param-value>WebKit|Opera|MSIE</param-value> 
        </init-param>
 </filter>
```

Map the filter on your web requests

```
 <filter-mapping>
   <filter-name>X</filter-name>
   <url-pattern>*</url-pattern>
 </filter-mapping>
```

# Init Parameters #

  * **ignoreURLPattern** - to ignore the URLs matching this regex. e.g. `.*\.(jpg|png|gif)`.
  * **acceptURLPattern** - to process the URLs matching this regex (ignore precedes). e.g. `.*\.(css|js|html)`.
  * **ignoreQueryStringPattern** - to ignore the URLs matching this query string regex. e.g. `.*\.(__DBG__=1)`.
  * **acceptQueryStringPattern** - to process the URLs matching this this query regex (ignore precedes). e.g. `.__wu__=1`.
  * **ignoreMIMEPattern** - to ignore if the response mime matches this regex. e.g. `images/.*|video/.*`.
  * **acceptMIMEPattern** - to process if the response mime matches this regex (ignore precedes). e.g. `text/css|text/html`.
  * **ignoreUAPattern** - to ignore if request user agent name matches this regex. e.g. `MSIE|KHTML`.
  * **acceptUAPattern** - to process if request user agent name matches this regex (ignore precedes). e.g. `WebKit|Opera`.

## About these patterns ##

  * If ignore pattern is not specified, it is treated as nothing to ignore.
  * If accept pattern is not specified, it is treated as everything to accept.
  * If resource matches both ignore and accept, ignore will take precedence.
  * If resource matches ignore pattern but not accept pattern, obviously it will not be processed by the filter.
  * If resource doesn't match ignore pattern but match accept pattern, then it will be processed by the filter.
  * If resource doesn't match ignore as well as accept pattern, it will not be processed.
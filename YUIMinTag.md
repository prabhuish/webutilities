If your page contains `<script>` and `<style>` tags containing JS and CSS code blocks, you may prefer to minify that code blocks as well to reduce the page size. `YUIMinTag` can help you with that.

**[YUIMinTag](YUIMinTag.md)** is the JSP custom tag to expose [YUICompressor](http://developer.yahoo.com/yui/compressor/) functionality in the JSP to minify/compress inline CSS, JS code blocks.



# Configuration #

Declare the taglib and prefix in your JSP file.

```
<%@ taglib uri="http://webutilities.googlecode.com/taglib/wu" prefix="wu" %>
```

# Usage #

Then use the **wu:minify** tag to minify your inline JS

```
 <wu:minify type="js">
        //...
  	// your inline uncompressed JS
  	//... 	
 </wu:minify>
```

OR CSS.

```
 <wu:minify type="css">
  	//...
  	// your inline uncompressed CSS
  	//...
 </wu:minify>
```

# Customization #

It supports attributes similar to YUICompressor's command line options. Below are the attributes and their explanations. All these attributes are optional except **type**.

  * **type** - possible values are js or css. The only required attribute. Usage as seen above.
  * **lineBreak** - equivalent to YUICompressor --line-break. Insert a line break after the specified column number
  * **noMunge** - equivalent to YUICompressor --nomunge. Minify only, do not obfuscate. Default false.
  * **preserveSemi** - equivalent to YUICompressor --preserve-semi. Preserve all semicolons. Default false.
  * **disableOptimizations** - equivalent to YUICompressor --disable-optimizations. Disable all micro optimizations. Default false.
  * **charset** - equivalent to YUICompressor --charset. Charset to be used. Default UTF-8.

Besides above parameters, each filter has following common parameters to better customize and configure it.

  * **ignoreURLPattern** - to ignore the URLs matching this regex. e.g. `.*\.(jpg|png|gif)`.
  * **acceptURLPattern** - to process the URLs matching this regex (ignore precedes). e.g. `.*\.(css|js|html)`.
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
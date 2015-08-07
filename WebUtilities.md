
**<= Use left sidebar for each component/feature details, configuration and customization**
## Introduction ##
Client side performance is important for better user experience. Optimizing and efficiently serving the static resources (JS, HTML, CSS, Images etc.) significantly increases client side performance. This Java Library (WebUtilities) provides web components to help you speed up Front-End of your J2EE application.

It is said that 80% of the end-user response time is spent on the front-end. To make the front-end efficient and friendly to the browser, [various performance practices](http://developer.yahoo.com/performance/rules.html) have been suggested. We can measure page performance using tools such as [YSlow](http://developer.yahoo.com/yslow/) or [Page Speed](http://code.google.com/speed/page-speed/). These tools validate page against the best practices and give the performance ratings/grade. WebUtilities provides inbuilt components to apply some of those best practices in your web application with minimal change to speed it up and get higher performance score. Below screenshots shows the difference it makes.

<table cellpadding='10' width='100%' align='center' border='0'>
<blockquote><tr><th>Before - Without WebUtilities</th><th>After - Using WebUtilities</th></tr>
<tr>
<blockquote><th>
<img src='http://webutilities.googlecode.com/svn/trunk/src/test/resources/img/BEFORE.png' />
</th>
<th>
<img src='http://webutilities.googlecode.com/svn/trunk/src/test/resources/img/AFTER.png' />
</th>
</blockquote></tr>
</table></blockquote>

## Features ##

  * Serve multiple JS or CSS files in one request
  * Add Expires header for JS, CSS and Image files to be cached by browser
  * Minify JS, CSS files on the fly
  * Minify Inline CSS and JS code blocks
  * Add Character Encoding to your response
  * Server compressed contents (gzip/compress/deflate)
  * Cache responses to speed loading by avoiding reprocessing

Let's see how to apply those best practices in your application and speed it up :)

## Get started ##

**For Examples and step by step Guide, Visit [Wiki](TableOfContents.md). Please Refer section on the left.**

## Dependency ##

For exact dependencies, please refer maven repository at http://maven-repository.com/artifact/com.googlecode.webutilities/webutilities.

**Use left navigation to get the configuration, usage and customization of each component in details.**
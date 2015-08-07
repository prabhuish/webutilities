<table cellpadding='3' cellspacing='0' align='right' border='0' valign='top'>
<tr><td valign='top'>
<b><i>News & Updates</i></b> <br />
<b>May 11, 2014</b>
<ul><li>New version <b><a href='https://github.com/rpatil26/webutilities/releases/tag/webutilities-0.0.7'>webutilities-0.0.7</a></b> released.<br>
</li><li>Available in <a href='http://search.maven.org/#artifactdetails%7Ccom.googlecode.webutilities%7Cwebutilities%7C0.0.7%7Cjar'>Maven Central</a> repository.<br>
</li><li>List of <a href='https://code.google.com/p/webutilities/issues/list?can=1&q=Milestone%3D0.0.7'>Issues Fixed</a> in this release.<br>
</li><li>Thanks to the <a href='https://github.com/rpatil26/webutilities/graphs/contributors'>Contributors</a>.<br>
<b>Mar 29, 2013</b>
</li><li>Released new version <b><a href='http://webutilities.googlecode.com/files/webutilities-0.0.6.jar'>webutilities-0.0.6</a></b>.<br>
</li><li>Available in <a href='http://search.maven.org/#artifactdetails%7Ccom.googlecode.webutilities%7Cwebutilities%7C0.0.6%7Cjar'>Maven Central</a> repository.<br>
</li><li>This is the <a href='https://code.google.com/p/webutilities/issues/list?can=1&q=Milestone%3D0.0.6+status%3AFixed'>list of fixes/enhancements</a> in this release.<br>
<b>Jan 28, 2012</b>
</li><li>Active source code repository is on github now<br>
</li><li><a href='https://github.com/rpatil26/webutilities'>https://github.com/rpatil26/webutilities</a>
<b>Nov 9, 2011</b>
</li><li><a href='http://webutilities.googlecode.com/files/webutilities-0.0.5.jar'>webutilities-0.0.5</a> has been released today.<br>
</li><li>Visit ChangeLog for details.<br>
</li><li><a href='WebUtilities.md'>Wiki docs</a> will be updated soon.<br>
</li><li>Also available in <a href='http://search.maven.org/#search%7Cga%7C1%7Cwebutilities'>Maven Central</a>
<b>Nov 5, 2011</b>
</li><li>Long awaited release <b>0.0.5</b> is coming soon.<br>
</li><li>Please help me test <b>0.0.5</b>.<br>
</li><li>Available <a href='https://oss.sonatype.org/content/repositories/comgooglecodewebutilities-012/com/googlecode/webutilities/webutilities/0.0.5/'>here</a> as oss sonatype maven repo.<br>
</li><li><a href='http://code.google.com/p/webutilities/issues/entry'>Report issues</a> if you found any.<br>
</td></tr>
<tr><td><wiki:gadget url="http://www.ohloh.net/p/586772/widgets/project_basic_stats.xml" height="210" border="0"/></td></tr></table></li></ul>

WebUtilities is the Java library that helps you to speed up and improve client side performance of your J2EE web application.



## Introduction ##
Client side performance is important for better user experience. Optimizing and efficiently serving the static resources (JS, HTML, CSS, Images etc.) significantly increases client side performance. This Java Library (WebUtilities) provides web components to help you speed up Front-End of your J2EE application.

It is said that 80% of the end-user response time is spent on the front-end. To make the front-end efficient and friendly to the browser, [various performance practices](http://developer.yahoo.com/performance/rules.html) have been suggested. We can measure page performance using tools such as [YSlow](http://developer.yahoo.com/yslow/) or [Page Speed](http://code.google.com/speed/page-speed/). These tools validate page against the best practices and give the performance ratings/grade. WebUtilities provides inbuilt components to apply some of those best practices in your web application with minimal change to speed it up and get higher performance score. Below screenshots shows the difference it makes.

<table cellpadding='20' border='0' align='left' cellspacing='30'>
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

## Features [:: Details](https://code.google.com/p/webutilities/wiki/TableOfContents) ##

  * Serve multiple JS or CSS files in one request
  * Add Expires header for JS, CSS and Image files to be cached by browser
  * Minify JS, CSS files on the fly
  * Minify Inline CSS and JS code blocks
  * Add Character Encoding to your response
  * Server compressed contents (gzip/compress/deflate)
  * Cache responses to speed loading by avoiding reprocessing

Let's see how to apply those best practices in your application and speed it up :)

## Get started [::Download](https://code.google.com/p/webutilities/downloads/list) ##
  * Refer Wiki here https://code.google.com/p/webutilities/wiki/WebUtilities
  * Configure your web.xml with [chain of filters](http://code.google.com/p/webutilities/wiki/ChainingOrder) accordingly.

**For Examples and step by step Guide, Visit [Wiki](WebUtilities.md).** For any issues or have feature suggestions, report them [here](http://code.google.com/p/webutilities/issues/entry).

## Dependencies ##

WebUtilities uses Maven to manage the dependencies. Please refer [POM details](http://search.maven.org/#artifactdetails%7Ccom.googlecode.webutilities%7Cwebutilities%7C0.0.7%7Cjar) for the list of dependencies.

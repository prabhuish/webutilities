We can cache the resources at client side using Cache-Control and Expires header using JSCSSMergeServelet. However sometimes if client cache is disabled by user, the resources get read from disk again and then served. Disk operations are costly. In our case when we can chain the performance filters like merging (JSCSSMergeServlet) , minifying (YUIMinFilter) and then compressing (CompressionFilter). New request for the same resources will have to go through each filter though we had already performed those optimization few minutes/seconds ago. In such cases having caching mechanism at server side improves significant performance.

**ResponseCacheFilter** is meant to serve that purpose. It caches the previously merged, minified and gziped response and serves from the cache next time. If any of resource in the request have been modified on the disk since last caching time, it also smartly reloads the cache with fresh contents and returns updated contents.

## Configuration ##

Declare this Filter in your web.xml ( web descriptor file)

```
<filter>
        <filter-name>responseCacheFilter</filter-name>
        <filter-class>com.googlecode.webutilities.filters.ResponseCacheFilter</filter-class>
 </filter>
```

Map this filter on your JS and CSS resources.

```
<filter-mapping>
   <filter-name>responseCacheFilter</filter-name>
   <url-pattern>*.js</url-pattern>
   <url-pattern>*.json</url-pattern>
   <url-pattern>*.css</url-pattern>
 </filter-mapping>
```

## Usage ##

Nothing much. Requested JS and CSS will pass through this Servlet and will get cached until it get modified on the disk. All subsequent responses will be much faster due to caching.

## Customization ##

  * **reloadTime** - interval in seconds after which resource cache will be reloaded
  * **resetTime** - interval in seconds after which whole cache will be cleared

Besides above parameters, each filter has [these  common init parameters](CommonFilterParameters.md) to better customize and configure it.

### URL parameters ###

Sometimes you may not want to use cache or you may want to evict the cache. Using below mentioned URL parameters you can do that.

**URL Parameters to skip or evict the cache**

  * **`_skipcache_`** - The JS or CSS request URL if contains this parameters the cache will not be used for it.
  * **`_dbg_`**- same as above _skipcache_ parameter.
  * **`_expirecache_`** - The cache for requested resource will be cleared.
  * **`_resetcache_`** - The whole cache will be reseted and all contents will cleared from cache

> Eg.
```
 <link rel="StyleSheet" href="/myapp/css/common.css?_dbg_=1"/>
```
> or
```
 <script language="JavaScript" src="/myapp/js/prototype.js?_expirecache_=1"></script>
```
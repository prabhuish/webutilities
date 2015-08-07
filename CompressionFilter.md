[Enabling Compression](http://developer.yahoo.com/performance/rules.html#gzip) reduces transfer size of the resources.  This can significantly reduce the time to send resources over the network because contents will be transferred in compressed format. There are various compression encodings like `gzip, deflate, compress` etc. HTTP request initiated by browser contains the information about whether browser is capable to handle the compressed contents. This is specified using `Accept-Encoding` HTTP header and it contains list of compressions supported by browser and also accepted quality factor (q). Server then can send the compressed response and specify compression encoding in `Content-Encoding` header of the response. Some clients may even be able to able to send request data itself in compressed format and in that case request `Content-Encoding` will specify the compression encoding.

**[CompressionFilter](CompressionFilter.md)** supports two way compression. It can uncompress the requests if compressed and can also respond with compressed contents to the requests who accept compressed contents (`Accept-Encoding`). Currently it implements three compression encodings - `gzip, compress and deflate`.

## Configuration ##

Declare this Filter in your web.xml ( web descriptor file)
```

<filter>
        <filter-name>compressionFilter</filter-name>
        <filter-class>com.googlecode.webutilities.filters.CompressionFilter</filter-class>
        <init-param> 
                <param-name>compressionThreshold</param-name>
                <param-value>1024</param-value> <!-- compress anything above 1kb -->
        </init-param>
        <init-param> 
                <param-name>ignoreURLPattern</param-name>
                <param-value>.*\.(flv|mp3|mpg)</param-value> <!-- regex -->
        </init-param>
        <init-param> 
                <param-name>ignoreMIMEPattern</param-name>
                <param-value>image/.*|video/.*|multipart/x-gzip</param-value> <!-- ignore -->
        </init-param>
        <init-param> 
                <param-name>ignoreUserAgentsPattern</param-name>
                <param-value>.*MSIE.*</param-value> <!-- regex -->
        </init-param>
 </filter>

```
Map this filter on your web requests
```
 <filter-mapping>
   <filter-name>compressionFilter</filter-name>
   <url-pattern>*</url-pattern>
 </filter-mapping>
```
## Usage ##

Nothing needed. As configured above, resources meeting the compression criteria will be compressed with appropriate compression encoding.

## Customization ##

It can be customized using the init parameters.

  * **compressionThreshold** - Resource of size larger than this bytes will be compressed.
  * **decompressMaxBytesPerSecond** - Max decompression rate (bytes per second) for compressed http request (since v0.0.7)
  * **maxDecompressedRequestSizeInBytes** - Max decompressed request size. If the request payload is larger than this then decompression throws IO Exception. (since v0.0.7)

Besides above parameters, each filter has [these  common init parameters](CommonFilterParameters.md) to better customize and configure it.
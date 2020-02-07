# AWS S3 Bucket Browser
S3 Bucket index.html to browse bucket content

![-](favicon.ico)

## [Demo](https://qoomon.github.io/aws-s3-bucket-browser/index.html?bucket=https://s3.eu-west-1.amazonaws.com/data.openspending.org)

## Installation

* Just <a download href="https://raw.githubusercontent.com/qoomon/aws-s3-bucket-browser/master/index.html">download</a> `index.html`  and put at root level of S3 bucket.
  * Adjust config within `index.html` if needed.
    * `title` - string
    * `subtitle` - string
    * `logo` - location
    * `favicon` - location
    * `keyExcludePattern`  - regex
    * `pageSize` - number

* Open `<S3_BUCKET_URL>/index.html` in your browser.

**or**

* Open hosted `index.html` and passing bucket parameter like this `<INDEX_FILE_LOCATION>?bucket=<S3_BUCKET_URL>` in your browser
  * **ensure CORS policy headers for S3 bucket**
* e.g. [`https://qoomon.github.io/aws-s3-bucket-browser/index.html?bucket=https://s3.eu-west-1.amazonaws.com/data.openspending.org`](https://qoomon.github.io/aws-s3-bucket-browser/index.html?bucket=https://s3.eu-west-1.amazonaws.com/data.openspending.org)


### CloudFront Setup
If you use CloudFront in upfront of your S3 bucket ensure following CloudFront settings.
- Allowed/Cached HTTP Methods: `GET`, `HEAD`, `OPTIONS`
- Cached Based on Selected Headers: `Whitelist`
  - `Access-Control-Request-Headers`
  - `Access-Control-Request-Methods`
  - `Origin`
- Query String Forwarding and Caching: `Forward all`

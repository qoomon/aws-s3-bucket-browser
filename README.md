# AWS S3 Bucket Browser
S3 Bucket index.html to browse bucket content

![](favicon.ico)

## [Demo](https://qoomon.github.io/aws-s3-bucket-browser/?bucket=https://s3.eu-west-1.amazonaws.com/data.openspending.org)

## Instalation

* Just <a download href="https://raw.githubusercontent.com/qoomon/aws-s3-bucket-browser/master/index.html">download</a> `index.html`  and put at root level of S3 bucket.
* Adjust config within `index.html` if needed.
  * `title`
  * `subtitle`,
  * `logo`
  * `favicon`
  * `keyExcludePattern` 
  * `pageSize`

* Open `<S3_BUCKET_URL>/index.html` in your browser.

**or**

* Open hosted `index.html` and passing bucket parameter like this `https://qoomon.github.io/aws-s3-bucket-browser/?bucket=<S3_BUCKET_URL>` in your browser
* **ensure CORS policy headers for S3 bucket**
* e.g. `https://qoomon.github.io/aws-s3-bucket-browser/?bucket=https://s3.eu-west-1.amazonaws.com/data.openspending.org`

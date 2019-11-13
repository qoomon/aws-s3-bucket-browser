# AWS S3 Bucket Browser
S3 Bucket index.html to browse bucket content

**[Demo](https://qoomon.github.io/aws-s3-bucket-browser/?bucket=https://s3.eu-west-1.amazonaws.com/data.openspending.org)**

## Instalation

* Just put the `index.html` into root level of S3 bucket.
* Adjust `titel`, `subtitle`, `logoUrl` and `pageSize` within `index.html` if needed.
* Open `<S3_BUCKET_URL>/index.html` in your browser.

**or**

* Open hosted `index.html` and passing bucket parameter like this `https://qoomon.github.io/aws-s3-bucket-browser/?bucket=<S3_BUCKET_URL>` in your browser
* **ensure CORS policy headers for S3 bucket**
* e.g. `https://qoomon.github.io/aws-s3-bucket-browser/?bucket=https://s3.eu-west-1.amazonaws.com/data.openspending.org`

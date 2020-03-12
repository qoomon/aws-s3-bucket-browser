# AWS S3 Bucket Browser
S3 Bucket index.html to browse bucket content

![-](favicon.ico)

## [Demo](https://qoomon.github.io/aws-s3-bucket-browser/index.html?bucket=https://s3.eu-west-1.amazonaws.com/data.openspending.org)

## Installation

#### Self-Hosted
* Just <a download href="https://raw.githubusercontent.com/qoomon/aws-s3-bucket-browser/master/index.html">download</a> `index.html` and put at root level of S3 bucket.
  * Adjust config within `index.html` if needed.
    * `title` - string
    * `subtitle` - string
    * `logo` - location
    * `favicon` - location
    * `keyExcludePattern`  - regex
    * `pageSize` - number
* **Ensure following Bucket Permissions**
  * Go to `https://s3.console.aws.amazon.com/s3/buckets/<YOUR BUCKET NAME>/?tab=permissions`
  * Grant public read permission by `Access Control List` or `Bucket Policy`
    * `Access Control List` Configuration
      * Enable `List objects` for `Everyone`
    * `Bucket Policy` Configuration
      ```json
      {
          "Version": "2012-10-17",
          "Statement": [
              {
                  "Sid": "PublicRead",
                  "Principal": "*",
                  "Effect": "Allow",
                  "Action": [
                      "s3:ListBucket",
                      "s3:GetObject"
                  ],
                  "Resource": [
                      "arn:aws:s3:::<YOUR BUCKET NAME>",
                      "arn:aws:s3:::<YOUR BUCKET NAME>/*"
                  ]
              }
          ]
      }
      ```
* Open `<YOUR BUCKET URL>/index.html` in your browser.

#### Hosted
* **Ensure following Bucket Permissions**
  * Go to `https://s3.console.aws.amazon.com/s3/buckets/<YOUR BUCKET NAME>/?tab=permissions`
  * Grant public read permission by `Access Control List` or `Bucket Policy`
    * see [Self-Hosted](#self-hosted)
  * Grant Cross Origin Access by `CORS Configuration`
    ```xml
    <!-- Sample policy -->
    <CORSConfiguration>
     <CORSRule>
      <AllowedOrigin>*</AllowedOrigin>
      <AllowedMethod>GET</AllowedMethod>
      <MaxAgeSeconds>3000</MaxAgeSeconds>
      <AllowedHeader>Authorization</AllowedHeader>
     </CORSRule>
    </CORSConfiguration>
    ```
* Open hosted `index.html` in your browser and passing bucket parameter
  * `<INDEX_FILE_LOCATION>?bucket=<S3_BUCKET_URL>` 
  * e.g. [`https://qoomon.github.io/aws-s3-bucket-browser/index.html?bucket=https://s3.eu-west-1.amazonaws.com/data.openspending.org`](https://qoomon.github.io/aws-s3-bucket-browser/index.html?bucket=https://s3.eu-west-1.amazonaws.com/data.openspending.org)


### CloudFront Setup
If you use CloudFront in upfront of your S3 bucket ensure following CloudFront settings.
- Allowed/Cached HTTP Methods: `GET`, `HEAD`, `OPTIONS`
- Cached Based on Selected Headers: `Whitelist`
  - `Access-Control-Request-Headers`
  - `Access-Control-Request-Methods`
  - `Origin`
- Query String Forwarding and Caching: `Forward all`

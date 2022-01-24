# AWS S3 Bucket Browser [![Sparkline](https://stars.medv.io/qoomon/aws-s3-bucket-browser.svg)](https://stars.medv.io/qoomon/aws-s3-bucket-browser)
![-](favicon.ico)

Single HTML file to browse AWS S3 buckets
## [Demo](https://qoomon.github.io/aws-s3-bucket-browser/index.html?bucket=https://s3.eu-west-1.amazonaws.com/data.openspending.org#worldbank/)

## Installation

#### Self-Hosted
* Just download [`index.html`](index.html) and upload it to your bucket.
  * Adjust [config](index.html#L8-L37) within `index.html` if needed, e.g.
    ```js
    const config = {
      title: 'Bucket Browser',
      subtitle: 'made with ♥ by qoomon',
      logo: 'https://qoomon.github.io/aws-s3-bucket-browser/logo.png',
      favicon: 'https://qoomon.github.io/aws-s3-bucket-browser/favicon.ico',
      primaryColor: '#167df0',
      
      bucketUrl: undefined,
      // If bucketUrl is undefined, this script tries to determine bucket Rest API URL from this file location itself.
      //   This will only work for locations like these
      //   * https://s3.BUCKET-REGION.amazonaws.com/BUCKET-NAME/index.html
      //   * http://BUCKET-NAME.s3-website-BUCKET-REGION.amazonaws.com/index.html
      //   * https://storage.googleapis.com/BUCKET-NAME/index.html
      // If bucketUrl is set manually, ensure this is the bucket Rest API URL, e.g.
      //   * https://s3.BUCKET-REGION.amazonaws.com/BUCKET-NAME
      //   * https://storage.googleapis.com/BUCKET-NAME
      //   The URL should return an XML document with <ListBucketResult> as root element.
      rootPrefix: undefined, // e.g. 'subfolder/'
      keyExcludePatterns: [/^index\.html$/],
      pageSize: 50,
      
      bucketMaskUrl: undefined, 
      // If bucketMaskUrl is set file urls will be changed from ${bucketUrl}/${file} to ${bucketMaskUrl}/${file}
      //   bucketMaskUrl: 'https://example.org'
      //     => https://example.org/foo/bar.txt 
      //   bucketMaskUrl: document.location.origin
      //     => ${document.location.origin}/foo/bar.txt 
      
      defaultOrder: 'name-asc' // (name|size|dateModified)-(asc|desc)
    }
    ```
* ⚠️ Ensure following Bucket Permissions
  * Go to `https://s3.console.aws.amazon.com/s3/buckets/<YOUR BUCKET NAME>/?tab=permissions`
  * Grant public read permission by `Access Control List` or `Bucket Policy`
    * Access Control List
      * Enable `List objects` for `Everyone`
    * Bucket Policy
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
* ⚠️ Ensure following Bucket Permissions
  * Go to `https://s3.console.aws.amazon.com/s3/buckets/<YOUR BUCKET NAME>/?tab=permissions`
  * Grant public read permission by `Access Control List` or `Bucket Policy`
    * see [Self-Hosted](#self-hosted)
  * Grant Cross Origin Access by `CORS Configuration`
    ```json
    [
    {
        "AllowedHeaders": [
            "*"
        ],
        "AllowedMethods": [
            "GET"
        ],
        "AllowedOrigins": [
            "http://www.example.com"
        ],
        "ExposeHeaders": [
            "x-amz-server-side-encryption",
            "x-amz-request-id",
            "x-amz-id-2"
        ],
        "MaxAgeSeconds": 3000
    }
    ]
    ```
* Open hosted `index.html` in your browser and provide bucket url as `bucket` request parameter
  * `${INDEX_FILE_LOCATION}?bucket=${S3_BUCKET_URL}` 
  * e.g. [`https://qoomon.github.io/aws-s3-bucket-browser/index.html?bucket=https://s3.eu-west-1.amazonaws.com/data.openspending.org`](https://qoomon.github.io/aws-s3-bucket-browser/index.html?bucket=https://s3.eu-west-1.amazonaws.com/data.openspending.org)


### CloudFront Setup
If you use CloudFront in upfront of your S3 bucket ensure following CloudFront settings.
- Allowed/Cached HTTP Methods: `GET`, `HEAD`, `OPTIONS`
- Cached Based on Selected Headers: `Whitelist`
  - `Access-Control-Request-Headers`
  - `Access-Control-Request-Method`
  - `Origin`
- Query String Forwarding and Caching: `Forward all`

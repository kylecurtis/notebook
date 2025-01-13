## **Learning Outcomes**

Through this assignment, you will:

- Articulate the characteristics of the AWS cloud computing platform.
- Describe the core benefits of using AWS products and services.
- Compare and contrast AWS cloud services to On-Premises infrastructure.
- Implement hosting a static web page using Amazon S3.
- Identify container services that are available for serverless computing.

---

## Game Notes

- AWS = Amazon Simple Storage Service
- Scripts that must run on web server = server-side scripts.
- A website that doesn't run server-side scripts = static website.
- Static website = Amazon S3 Bucket with static website hosting feature.
- S3 buckets are automatically replicated across multiple AWS data centers for high resiliency.
- In Amazon S3, any type of file/metadata that describes a file is called an object.
- Objects are stored in S3 containers called buckets.
- When an S3 bucket is configure for web hosting, the bucket is assigned a URL.
- For others to access the S3 bucket, a bucket policy can be created to configure permissions.
- Bucket policies are written in JSON format.
- You can choose the geographical AWS region where S3 stores the buckets.
- Objects stored in an AWS region never leave unless you explicitly transfer or replicate them to another region.
- S3 can upload objects up to 5GB with a single PUT operation. Larger objects up to 5TB use the multipart upload API.
- By default, all S3 resources are private (only resource owner can grant access permissions w/ access policy).

---

## Game Steps

- Search for and go to S3 service
- Click on the bucket called: "website-bucket-*"
- Click on "text.html" and rename object to "error.html"
- Click on the Permissions tab
- Set block all public access to "Off"
- Click on Properties tab
- Scroll down to static website hosting and click Edit
- Enable static website hosting and select Host a static website
- Index document = index.html, Error document = error.html
- Save changes
- Check Static website hosting options for Bucket hosting type
- Under Bucket website endpoint, click copy icon
- Paste endpoint into a browser tab
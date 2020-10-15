# AWS-s3-bucket-security-config
AWS-s3-bucket-security-config
.



Go to AWS S3 bucket Service

Then click on a bucket you want to alter permissions for

Ref link for same : https://docs.aws.amazon.com/AmazonS3/latest/dev/example-walkthroughs-managing-access-example1.html 


After going to Bucket 

Follow the steps :

Bucket Permissions (inside a specific bucket) ==>  Block all public Access ==> Bucket Policy ( Add the below thing ) ==> CROS POLICY

Bucket Policy:
```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "",
            "Effect": "Allow",
            "Principal": {
                "AWS": "Go TO IAM and paste the USer ARN ID here"
            },
            "Action": [
                "s3:PutObjectAcl",
                "s3:PutObject"
            ],
            "Resource": "bucket Name/*"
        }
    ]
}
```
CROS POLICY:

```
<?xml version="1.0" encoding="UTF-8"?>
<CORSConfiguration xmlns="http://s3.amazonaws.com/doc/2006-03-01/">
<CORSRule>
    <AllowedOrigin>*</AllowedOrigin>
    <AllowedMethod>HEAD</AllowedMethod>
    <AllowedMethod>GET</AllowedMethod>
    <AllowedMethod>POST</AllowedMethod>
    <ExposeHeader>ETag</ExposeHeader>
    <AllowedHeader>*</AllowedHeader>
</CORSRule>
</CORSConfiguration>
```


You also need to Add Inline Policy in the IAM user Permission thing :

```
{
   "Version": "2012-10-17",
   "Statement": [
      {
         "Sid": "PermissionForObjectOperations",
         "Effect": "Allow",
         "Action": [
            "s3:PutObject"
         ],
         "Resource": [
            "arn:aws:s3:::awsexamplebucket1/*"
         ]
      }
   ]
}
```

# s3-bucket-browser
An single index.html file that - along with proper config - allows the visitor to browse through an S3 bucket

Note the URLs below and in the code are IP-restricted.  And even if you did get access to them all you'd see is a thousand pictures of my sons : )

Had to:

1) Create new Identity Pool using Cognito allowing unauthenticated identities
Make sure to check "Enable access to unauthenticated identities", but accept defaults otherwise

2) CORS Configuration
<?xml version="1.0" encoding="UTF-8"?>
<CORSConfiguration xmlns="http://s3.amazonaws.com/doc/2006-03-01/">
    <CORSRule>
        <AllowedOrigin>*</AllowedOrigin>
        <AllowedMethod>GET</AllowedMethod>
        <AllowedHeader>*</AllowedHeader>
    </CORSRule>
</CORSConfiguration>

3) Bucket Policy
{
        "Version": "2012-10-17",
        "Id": "S3PolicyId1",
        "Statement": [
                {
                        "Sid": "IPAllow",
                        "Effect": "Allow",
                        "Principal": "*",
                        "Action": "s3:*",
                        "Resource": "arn:aws:s3:::<bucket-name>/*",
                        "Condition": {
                                "IpAddress": {
                                        "aws:SourceIp": "<IP>/24"
                                }
                        }
                }
        ]
}

4) Grant "List" permissions to "Authenticated Users"

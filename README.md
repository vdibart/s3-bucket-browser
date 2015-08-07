# s3-bucket-browser
An single index.html file that - along with proper config - allows the visitor to browse through an S3 bucket

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
                        "Resource": "arn:aws:s3:::dibartolo-family-photos/*",
                        "Condition": {
                                "IpAddress": {
                                        "aws:SourceIp": "69.203.103.118/24"
                                }
                        }
                }
        ]
}

4) Grant "List" permissions to "Authenticated Users"

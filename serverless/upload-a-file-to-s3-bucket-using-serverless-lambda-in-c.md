# Upload a file to S3 bucket using serverless lambda in C\#

What a lengthy title, but it' is what I am going to do now.

### First, create a bucket in Cloudformation

Create a bucket and bucket policy with CloudFormation

```yaml
resources:
  Resources:
    attachmentsBucket:
      Type: AWS::S3::Bucket
      Properties:
        BucketName: xxxxxx-attachments
        AccessControl: Private
        CorsConfiguration:
          CorsRules:
            - AllowedMethods:
                - GET
                - PUT
                - POST
                - HEAD
              AllowedOrigins:
                - "*"
              AllowedHeaders:
                - "*"

    attachmentsBucketPolicy:
      Type: AWS::S3::BucketPolicy
      Properties:
        Bucket:
          Ref: attachmentsBucket
        PolicyDocument:
          Statement:
            - Effect: Allow
              Principal: '*'
              Action:
                - "s3:PutObject"
                - "s3:PutObjectAcl"
              Resource: "arn:aws:s3:::xxxxxx-attachments/*"

```

### Upload the file in c\#

We need to reference a package, `AWSSDK.S3` 




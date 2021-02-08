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
        BucketName: xxxx-attachments-${opt:stage, self:provider.stage}
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
                - "s3:GetObject"
              Resource: "arn:aws:s3:::xxxx-attachments-${opt:stage, self:provider.stage}/*"
            - Effect: Allow
              Principal:
                AWS: 
                  - Fn::GetAtt: [ IamRoleLambdaExecution, Arn ]
              Action:
                - "s3:PutObject"
                - "s3:PutObjectAcl"
                - "s3:GetObject"
              Resource: "arn:aws:s3:::xxxx-attachments-${opt:stage, self:provider.stage}/*"

```

As it's a public bucket, it allows `s3:GetObject` to everyone \(`Principal:'*'`\). Yet, only `IamRoleLambdaExecution` can upload the file. 

### Pre-signed url






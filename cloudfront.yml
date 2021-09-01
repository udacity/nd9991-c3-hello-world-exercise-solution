Parameters:
  # Existing Bucket name
  PipelineID:
    Description: Existing Bucket name
    Type: String

Resources:
  CloudFrontOriginAccessIdentity:
    Type: "AWS::CloudFront::CloudFrontOriginAccessIdentity"
    Properties:
      CloudFrontOriginAccessIdentityConfig:
        Comment: Origin Access Identity for Serverless Static Website

  WebpageCDN:
    Type: AWS::CloudFront::Distribution
    Properties:
      DistributionConfig:
        Origins:
          - DomainName: !Sub "${PipelineID}.s3.amazonaws.com"
            Id: webpage
            S3OriginConfig:
              OriginAccessIdentity: !Sub "origin-access-identity/cloudfront/${CloudFrontOriginAccessIdentity}"
        Enabled: True
        DefaultRootObject: index.html
        DefaultCacheBehavior:
          ForwardedValues:
            QueryString: False
          TargetOriginId: webpage
          ViewerProtocolPolicy: allow-all

Outputs:
  PipelineID:
    Value: !Sub ${PipelineID}
    Export:
      Name: PipelineID
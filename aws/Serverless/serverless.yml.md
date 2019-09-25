```yml
service:
  name: myService

frameworkVersion: '>=1.0.0 <2.0.0'

provider:
  name: aws
  runtime: nodejs10.x
  stage: ${opt:stage, 'dev'} # Set the default stage used. Default is dev
  region: ${opt:region, 'us-east-1'} # Overwrite the default region used. Default is us-east-1
  stackName: custom-stack-name # Use a custom name for the CloudFormation stack
  apiName: custom-api-name # Use a custom name for the API Gateway API
  memorySize: 512 # Overwrite the default memory size. Default is 1024
  timeout: 10 # The default is 6 seconds. Note: API Gateway current maximum is 30 seconds
  logRetentionInDays: 14 # Set the default RetentionInDays for a CloudWatch LogGroup
  environment: # Service wide environment variables
    serviceEnvVar: 123456789
  iamRoleStatements: # IAM role statements so that services can be accessed in the AWS account
    - Effect: 'Allow'
      Action:
        - 's3:ListBucket'
      Resource:
        Fn::Join:
          - ''
          - - 'arn:aws:s3:::'
            - Ref: ServerlessDeploymentBucket
  
functions:
  usersCreate: # A Function
    handler: users.create # The file and module for this specific function.
    name: ${self:provider.stage}-lambdaName # optional, Deployed Lambda name
    description: My function # The description of your function.
    memorySize: 512 # memorySize for this specific function.
    reservedConcurrency: 5 # optional, reserved concurrency limit for this function. By default, AWS uses account concurrency limit
    runtime: nodejs10.x # Runtime for this specific function. Overrides the default which is set on the provider level
    timeout: 10 # Timeout for this specific function.  Overrides the default set above.
    role: arn:aws:iam::XXXXXX:role/role # IAM role which will be used for this function
    onError: arn:aws:sns:us-east-1:XXXXXX:sns-topic # Optional SNS topic / SQS arn (Ref, Fn::GetAtt and Fn::ImportValue are supported as well) which will be used for the DeadLetterConfig
    awsKmsKeyArn: arn:aws:kms:us-east-1:XXXXXX:key/some-hash # Optional KMS key arn which will be used for encryption (overwrites the one defined on the service level)
    environment: # Function level environment variables
      functionEnvVar: 12345678
    tags: # Function specific tags
      foo: bar
    vpc: # Optional VPC. But if you use VPC then both subproperties (securityGroupIds and subnetIds) are required
      securityGroupIds:
        - securityGroupId1
        - securityGroupId2
      subnetIds:
        - subnetId1
        - subnetId2
    events: # The Events that trigger this Function
      - http: # This creates an API Gateway HTTP endpoint which can be used to trigger this function.  Learn more in "events/apigateway"
          path: users/create # Path for this endpoint
          method: get # HTTP method for this endpoint
          cors: true # Turn on CORS for this endpoint, but don't forget to return the right header in your response
          private: true # Requires clients to add API keys values in the `x-api-key` header of their request
          authorizer: # An AWS API Gateway custom authorizer function
            name: authorizerFunc # The name of the authorizer function (must be in this service)
            arn: xxx:xxx:Lambda-Name # Can be used instead of name to reference a function outside of service
            resultTtlInSeconds: 0
            identitySource: method.request.header.Authorization
            identityValidationExpression: someRegex
            type: token # token or request. Determines input to the authorier function, called with the auth token or the entire request event. Defaults to token
      - s3:
          bucket: photos
          event: s3:ObjectCreated:*
          rules:
            - prefix: uploads/
            - suffix: .jpg

# The "Resources" your "Functions" use.  Raw AWS CloudFormation goes in here.
resources:
  Resources:
    usersTable:
      Type: AWS::DynamoDB::Table
      Properties:
        TableName: usersTable
        AttributeDefinitions:
          - AttributeName: email
            AttributeType: S
        KeySchema:
          - AttributeName: email
            KeyType: HASH
        ProvisionedThroughput:
          ReadCapacityUnits: 1
          WriteCapacityUnits: 1
```

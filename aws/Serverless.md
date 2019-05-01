## Create DynamoDB
##### Create a table: **Products**
##### Get Amazon Resource Name (ARN)
> arn:aws:dynamodb:ap-northeast-1:845350057538:table/Products

## Create an execution role
- Select type of trusted entity: **Lambda**
- Filter policies: **AWS Lambda**
  - [x] **AWSLambdaBasicExecutionRole**
- Role name: **hexal-lambda-basic-execution**
- Add inline policies
  1. Service: **DynamoDB**
  2. Actions: **Add 4 manual actions**
    - [x] getItem
    - [x] putItem
    - [x] updateItem
    - [x] deleteItem

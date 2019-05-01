## Create DynamoDB
##### Create a table: **Products**
##### Get Amazon Resource Name (ARN)
> arn:aws:dynamodb:ap-northeast-1:845350057538:table/Products

## Create Role
##### Create an execution role
- Select type of trusted entity: **Lambda**
- Filter policies: **AWS Lambda**
  - [x] **AWSLambdaBasicExecutionRole**
- Role name: **hexal-lambda-basic-execution**
##### Add DynamoDB permissions
- Add inline policies
  - Service: **DynamoDB**
  - Actions: **Add 4 manual actions**
    - [x] getItem
    - [x] putItem
    - [x] updateItem
    - [x] deleteItem
  - Resources: **Add DynamoDB ARN**
- Create policy name: **hexal-dynamo-policy**

## Create Lambda Function
##### Create put function
- Function name: **hexlPut**
- Permissions: 
  - Execution role: **Use an existing role**
  - Existing role: **hexal-lambda-basic-execution**


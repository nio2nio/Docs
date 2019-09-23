### Add New User
- Login to AWS Account and go to the Identity & Access Management (IAM) page.
- Add a user
  - Enable **Programmatic access**
  - **Attach existing policies directly**
    - [x] **AdministratorAccess**
- View and copy the API Key & Secret to a temporary place.

### Using AWS Profiles
- Setup with **serverless config credentials**
```shell
$ serverless config credentials --provider aws --key ACCESS_KEY_ID --secret SECRET_ACCESS_KEY
```

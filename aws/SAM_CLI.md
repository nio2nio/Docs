## 1. Create an AWS account.

## 2. Configure IAM permissions.
+ Add user: **Administrator**
+ Add group: **Administrators**
  + Policies: **AdministratorAccess** (AWS Managed - job function)
 
 ## 3. Install and Configure the AWS CLI
 + Install the AWS CLI
 ```bash
$ curl "https://s3.amazonaws.com/aws-cli/awscli-bundle.zip" -o "awscli-bundle.zip"
$ unzip awscli-bundle.zip
$ sudo ./awscli-bundle/install -i /usr/local/aws -b /usr/local/bin/aws

$ /usr/local/bin/aws --version
```
+ Configure the AWS CLI
```bash
$ aws configure
AWS Access Key ID [None]: # Enter your access key
AWS Secret Access Key [None]: # Enter your secret key
Default region name [None]: # Example regions: us-east-1, ap-east-1, eu-central-1, sa-east-1
Default output format [None]: json
```

## 4. Create an Amazon S3 Bucket
```bash
$ aws s3 mb s3://bucket_name --region region

make_bucket: bucket_name
```

## 5. Install Docker
+ Uninstall old versions
```bash
$ sudo apt-get remove docker docker-engine docker.io containerd runc
```
+ Set up the repository
```bash
$ sudo apt-get update

# Install packages to allow apt to use a repository over HTTPS
$ sudo apt-get install \
    apt-transport-https \
    ca-certificates \
    curl \
    gnupg-agent \
    software-properties-common
    
# Add Docker's official GPG key:
$ curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -

# Verify GPG key with the fingerprint
$ sudo apt-key fingerprint 0EBFCD88
    
pub   rsa4096 2017-02-22 [SCEA]
      9DC8 5822 9FC7 DD38 854A  E2D8 8D81 803C 0EBF CD88
uid           [ unknown] Docker Release (CE deb) <docker@docker.com>
sub   rsa4096 2017-02-22 [S]

# Set up the stable repository
$ sudo add-apt-repository \
   "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
   $(lsb_release -cs) \
   stable"
```
+ Install docker engine
```bash
$ sudo apt-get update
$ sudo apt-get install docker-ce docker-ce-cli containerd.io
```
+ Start the Docker service
```bash
$ sudo systemctl start docker.service

# Execute Docker commands without using sudo
$ sudo usermod -a -G docker user
```

## 6. Install Homebrew
+ Install Homebrew
```bash
$ sh -c "$(curl -fsSL https://raw.githubusercontent.com/Linuxbrew/install/master/install.sh)"
```
+ add Homebrew to your PATH
```bash
$ test -d ~/.linuxbrew && eval $(~/.linuxbrew/bin/brew shellenv)
$ test -d /home/linuxbrew/.linuxbrew && eval $(/home/linuxbrew/.linuxbrew/bin/brew shellenv)
$ test -r ~/.bash_profile && echo "eval \$($(brew --prefix)/bin/brew shellenv)" >>~/.bash_profile
$ echo "eval \$($(brew --prefix)/bin/brew shellenv)" >>~/.profile

# Verify that Homebrew is installed
$ brew --version
```

## 7. Install the AWS SAM CLI
```bash
$ brew tap aws/tap
$ brew install aws-sam-cli

# Verify the installation
$ sam --version
```
```


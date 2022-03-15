# SETUP AWS CLI

## Install aws-cli using Homebrew on macOS

- Install [Homebrew](https://brew.sh) from the official website.

- To install aws-cli use the below command

    `$ brew install awscli`

## How to use the aws-cli?

- DevOps team will create a new username and password for you on Transreport AWS account

- Go to [aws console IAM service](https://console.aws.amazon.com/iam/home?#home) to get your credentials including

    1- AWS Access Key ID

    2- AWS Secret Access Key

- Then you can configure your aws-cli to use these credentials


        $ aws configure

        AWS Access Key ID [None]: AKIAIOSFODNN7EXAMPLE

        AWS Secret Access Key [None]: wJalrXUtnFEMI/K7MDENG/bPxRfiCYEXAMPLEKEY

        Default region name [None]: eu-west-2

        Default output format [None]: json
    

## Install aws-mfa

- You can install the aws-mfa tool through PIP

    `$ pip install aws-mfa`

- You have an aws credentials file located in `~/.aws/credentials`

    It will look like this:

    ```
    [example-profile-long-term]

    aws_access_key_id = YOUR_LONGTERM_KEY_ID

    aws_secret_access_key = YOUR_LONGTERM_ACCESS_KEY
    ```

- After running `aws-mfa --profile example-profile` aws-mfa will propigate the short term credentials to the file and it will look like this:

    ```
    [example-profile-long-term]
    aws_access_key_id = YOUR_LONGTERM_KEY_ID
    aws_secret_access_key = YOUR_LONGTERM_ACCESS_KEY

    [example-profile]
    aws_access_key_id = <POPULATED_BY_AWS-MFA>
    aws_secret_access_key = <POPULATED_BY_AWS-MFA>
    aws_security_token = <POPULATED_BY_AWS-MFA>
    ```

- [NOTE] Usually the mfa will require re-authentication every 24 hours, so if you are trying to access an aws service and its not working like `aws s3 ls` the first thing i would do is to make sure that i am already autheticated through aws-mfa.


- [NOTE] `aws-mfa --profile example-profile` We are using multi aws accounts now so you can specify a name of your aws profile here. The default profile name is `default`. The value can also be provided by the environment variable `AWS_PROFILE`.

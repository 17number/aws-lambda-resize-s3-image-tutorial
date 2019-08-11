# What is this

[チュートリアル: Amazon S3 で AWS Lambda を使用する \- AWS Lambda](https://docs.aws.amazon.com/ja_jp/lambda/latest/dg/with-s3-example.html) をベースに改造


# Requirements

## [aws-cli](https://github.com/aws/aws-cli)

### Install

```bash
$ pip install awscli
```

### Configuration

```bash
$ aws configure
AWS Access Key ID [None]: YourAccessKeyId
AWS Secret Access Key [None]: YourSecretAccessKey
Default region name [None]: ap-northeast-1  # 東京以外の場合は適宜変更
Default output format [None]: json  # json, text, table が選択可能
```


# Usage

## Install node modules

```bash
$ npm install
```


## Create lambda function

- Zip function code and `node_modules`.
- Upload by `aws lambda create-function`.
  - Edit parameters and role.

```bash
$ zip -r function.zip index.js node_modules
$ aws lambda create-function --function-name CreateThumbnail \
--zip-file fileb://function.zip \
--handler index.handler \
--runtime nodejs8.10 \
--timeout 10 \
--memory-size 1024 \
--role arn:aws:iam::123456789012:role/your-aws-role
```


### Update lambda function

- Exec `aws lambda update-function-code`.

```bash
$ aws lambda update-function-code --function-name CreateThumbnail --zip-file fileb://function.zip
```


### Test lambda function

```bash
$ aws lambda invoke --function-name CreateThumbnail --invocation-type Event --payload file://inputFile.txt outputFile.txt
```

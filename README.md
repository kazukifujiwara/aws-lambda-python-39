# aws-lambda-python-39

## run lambda function

### build image

```
docker build -t {IMAGE NAME} .  
```

### run container

```
docker run --rm -p 9000:8080 {IMAGE NAME}
```

### invoke lambda function

```
curl -d '{}' http://localhost:9000/2015-03-31/functions/function/invocations
```

## S3 Access

### run container

```
docker run --rm \
  -p 9000:8080 \
  -e AWS_ACCESS_KEY_ID={アクセスキー} \
  -e AWS_SECRET_ACCESS_KEY={シークレットキー} \
  -e AWS_DEFAULT_REGION={リージョン} \
  {イメージ名}
```

## AWS Create Repository

### Create Repository

```
aws ecr create-repository --repository-name [REPOSITORY_NAME] --profile [PROFILE]
```

### Tagging

```
docker tag [IMAGE_NAME]:latest ${ACCOUNTID}.dkr.ecr.${REGION}.amazonaws.com/[REPOSITORY_NAME]:latest
```

### Login test

```
aws ecr get-login-password --profile [PROFILE] | docker login --username AWS --password-stdin ${ACCOUNTID}.dkr.ecr.${REGION}.amazonaws.com
```

### Push iamge

```
docker push ${ACCOUNTID}.dkr.ecr.${REGION}.amazonaws.com/[REPOSITORY_NAME]:latest
```

## Reference 

* [コンテナイメージを使用してAWS Lambda関数を作成する](https://qiita.com/kyamamoto9120/items/f1cda89ffc7cb5254f17)
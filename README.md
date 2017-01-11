```
#!/bin/bash -ex

LABEL='backup-ebs-volumes-job'
TAG='0.0.1'

docker build . -t ${LABEL}:${TAG}

docker run \
  -e AWS_ACCESS_KEY_ID=${AWS_ACCESS_KEY_ID} \
  -e AWS_SECRET_ACCESS_KEY=${AWS_SECRET_ACCESS_KEY} \
  -e AWS_DEFAULT_REGION='us-east-1' \
  --rm \
  -t ${LABEL}:${TAG}

docker run \
  -e AWS_ACCESS_KEY_ID=${AWS_ACCESS_KEY_ID} \
  -e AWS_SECRET_ACCESS_KEY=${AWS_SECRET_ACCESS_KEY} \
  -e AWS_DEFAULT_REGION='us-east-1' \
  -e AWS_ACCOUNT_IDS='****' \
  --rm \
  -t ${LABEL}:${TAG} \
  python ebs-snapshot-janitor.py
  ```

# Github action CI CD

```js
name: CI-CD-Pipeline
env:
  EB_PACKAGE_S3_BUCKET: "S3"
  EB_APPLICATION: "EB_APP"
  EB_ENVIRONMENT: "EB_ENV"
  DEPLOY_PACKAGE: "deploy_${{github.sha}}.zip"
  AWS_REGION: "ap-northeast-2"

on:
  push:
    branch: [main]

jobs:
  CI:
    runs-on: ubuntu-latest
    
    steps:
      - name: Git clone repository
        uses: actions/checkout@v1
      
      - name: NPM Install
        run: npm ci
        
      - name: Build
        run: npm run build sms
      
      - name: Create ZIP deployment package
        run: zip -r ${{env.DEPLOY_PACKAGE}} ./ -x *.git*
      
      - name: Configure AWS Credentials
        uses: aws-actions/configure-aws-credentials@v1
        with:
          aws-access-key-id: ${{ secrets.AWS_ACCESS_KEY_DEV }}
          aws-secret-access-key: ${{ secrets.AWS_SECRET_KEY_DEV }}
          aws-region: ${{ env.AWS_REGION }}
      
      - name: Copy deployment package to S3 Bucket
        run: aws s3 cp ${{ env.DEPLOY_PACKAGE }} s3://${{ env.EB_PACKAGE_S3_BUCKET }}/

  CD:
    runs-on: ubuntu-latest
    needs: [CI]
    
    steps:
      - name: Configure AWS Credentials
        uses: aws-actions/configure-aws-credentials@v1
        with:
          aws-access-key-id: ${{ secrets.AWS_ACCESS_KEY_DEV }}
          aws-secret-access-key: ${{ secrets.AWS_SECRET_KEY_DEV }}
          aws-region: ${{ env.AWS_REGION }}
      - name: Create new EB Application version
        run: |
          APP_NAME="$(echo "${{github.ref}}" | grep -E -i -w -o 'sms|email|push')"
          echo "$APP_NAME"
          aws elasticbeanstalk create-application-version \
          --application-name ${{ env.EB_APPLICATION }}-$APP_NAME \
          --source-bundle S3Bucket="${{ env.EB_PACKAGE_S3_BUCKET }}",S3Key="${{ env.DEPLOY_PACKAGE }}" \
          --version-label "Ver-${{github.sha}}" \
          --description "CommitSHA-${{github.sha}}"
     
      - name: Deploy new EB Application version
        run: |
          APP_NAME="$(echo "${{github.ref}}" | grep -E -i -w -o 'sms|email|push')"
          echo "$APP_NAME"
          aws elasticbeanstalk update-environment \
          --environment-name ${{ env.EB_ENVIRONMENT }}-$APP_NAME \
          --version-label "Ver-${{github.sha}}"

```
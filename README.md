# SecureStack Log4j Vulnerability Analysis GitHub Action

A GitHub Action that analyses your java source code for all versions of the log4j vulnerability that affect both log4j 1.x and 2.x.  You can read more about all versions of Log4j that are affected here:  https://logging.apache.org/log4j/2.x/security.html

```
name: Example Workflow Using SecureStack All-In-One Action
on: push
jobs:
  security:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout repo for running secrets analysis within workflow
        id: checkout
        uses: actions/checkout@v2.4.0
        with:
          fetch-depth: 0
      - name: Secrets Analysis Step
        id: secrets
        uses: SecureStackCo/actions-secrets@v0.1.2
        with:
          securestack_api_key: ${{ secrets.SECURESTACK_API_KEY }}
          securestack_app_id: ${{ secrets.SECURESTACK_APP_ID }}
          severity: critical
          flags: '-d 1'
      - name: Code Analysis Step
        id: code
        uses: SecureStackCo/actions-code@v0.1.0
        with:
          securestack_api_key: ${{ secrets.SECURESTACK_API_KEY }}
          securestack_app_id: ${{ secrets.SECURESTACK_APP_ID }}
          severity: critical
          language: node
      - name: Exposure Analysis Step
        id: exposure
        uses: SecureStackCo/actions-exposure@v0.1.2
        with:
          securestack_api_key: ${{ secrets.SECURESTACK_API_KEY }}
          securestack_app_id: ${{ secrets.SECURESTACK_APP_ID }}
          severity: critical
          flags: '--dom -r'
```
## Create your SecureStack API Key as GitHub Secret

1. Log in to [SecureStack](https://app.securestack.com) and go to the Profile -> GENERATE KEY screen.
2. Generate an API key and copy the value.
3. Go to Settings for your GitHub repository and click on Secrets -> Actions at the bottom left.
4. Create a new secret named SECURESTACK_API_KEY and paste the value from step 2 into the field.

## Retreiving your SecureStack Application ID

1. Log in to [SecureStack](https://app.securestack.com).
2. Open the application you wish to analyse.
3. Copy the value of the application id on the View Application screen.
4. Go to Settings for your GitHub repository and click on Secrets -> Actions at the bottom left.
5. Create a new secret named SECURESTACK_APP_ID and paste the value from step 3 into the field.

### Watch this video to learn how to setup your first GitHub Action with SecureStack
[![IMAGE ALT TEXT](http://img.youtube.com/vi/0sYXsCmY2es/0.jpg)](http://www.youtube.com/watch?v=0sYXsCmY2es "Video Title")


## Check out our other GitHub Actions:
1. [SecureStack Secrets Analysis](https://github.com/marketplace/actions/securestack-secrets-analysis) - Scan your application for embedded api keys, credentials and senstive data.
2. [SecureStack Software Composition Analysis (SCA)](https://github.com/marketplace/actions/securestack-application-composition-analysis) - Scan your application for vulnerable third-party and open source libraries.
3. [SecureStack Web Vulnerability & Cloud Misconfiguration Analysis](https://github.com/marketplace/actions/securestack-application-composition-analysis) - Scan your running application url for cloud misconfigurations and web vulnerabilities.

Made with 💜  by [SecureStack](https://securestack.com)

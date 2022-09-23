# SecureStack - One Github Action To Rule Them All

This Action provides comprehensive security coverage for your entire GitHub project workflow! This is the SecureStack kitchen sink and combines 3 different GitHub Actions into one awesome Action to rule them all!  When you add this Action to your repository it will:

* Analyze source code for sensitive data like API keys, database credentials, passwords, etc
* Analyze source code for any vulnerable third-party or open source libraries with our software composition analysis  
* If your app is running in the public cloud we'll analyze it for cloud misconfigurations and inseure settings
* Finally, we will scan the public URL for your web app with our web vulnerability scanner

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
        uses: SecureStackCo/actions-secrets@v0.1.3
        with:
          securestack_api_key: ${{ secrets.SECURESTACK_API_KEY }}
          securestack_app_id: ${{ secrets.SECURESTACK_APP_ID }}
          severity: critical
          flags: '-d 1'
      - name: Code Analysis Step
        id: code
        uses: SecureStackCo/actions-code@v0.1.1
        with:
          securestack_api_key: ${{ secrets.SECURESTACK_API_KEY }}
          securestack_app_id: ${{ secrets.SECURESTACK_APP_ID }}
          severity: critical
          language: node
      - name: Exposure Analysis Step
        id: exposure
        uses: SecureStackCo/actions-exposure@v0.1.3
        with:
          securestack_api_key: ${{ secrets.SECURESTACK_API_KEY }}
          securestack_app_id: ${{ secrets.SECURESTACK_APP_ID }}
          severity: critical
          flags: '--dom -r'
      - name: Create SBOM
        id: sbom
        uses: SecureStackCo/actions-sbom@v0.1.1
        with:
          securestack_api_key: ${{ secrets.SECURESTACK_API_KEY }}
          securestack_app_id: ${{ secrets.SECURESTACK_APP_ID }}
          severity: critical
```
## Create your SecureStack API Key as GitHub Secret

1. Create a SecureStack account using your GitHub credentials. You get 20 scans for free and you don't need to add a credit card.
2. Once you are logged in go to "Settings" in the black drawer on the left, and then -> API tab.
3. Generate an API key and copy the value.
4. Go to Settings for your GitHub repository and click on Secrets -> Actions at the bottom left.
5. Create a new secret named SECURESTACK_API_KEY and paste the value from step 2 into the field.

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

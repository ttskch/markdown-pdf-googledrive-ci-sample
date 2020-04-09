# markdown-pdf-googledrive-ci-sample

A sample of converting Markdown to PDF and deploying to Google Drive with CircleCI 2.0

## Mechanism

* Converts Markdown to PDF with [markdown-pdf](https://github.com/alanshaw/markdown-pdf)
* Deploys PDF to Google Drive with [gdrive](https://github.com/gdrive-org/gdrive)
    * Uses [Service Account](https://github.com/gdrive-org/gdrive#service-account) feature to make CircleCI enable to deploy to Google Drive

## Preparing

### 1. Create a Service Account

1. Go to [Google API Console](https://console.developers.google.com/)
1. Create a new Service Account in some project
1. Download the credential json file

### 2. Register the credential of Service Account as an envvar on CircleCI

1. Make the credential json "one line" and copy it
1. Go to https://circleci.com/gh/{user}/{project}/edit#env-vars and add the copied credential as a new envvar named `GOOGLE_SERVICE_ACCOUNT_CREDENTIAL`
![image](https://user-images.githubusercontent.com/4360663/39964939-575c488a-56ca-11e8-8448-3880a79d79d3.png)

### 3. Allow the Service Account to access the target folder on Google Drive

1. [Show](https://console.developers.google.com/iam-admin/serviceaccounts) the email address of the Service Account and copy it
![image](https://user-images.githubusercontent.com/4360663/39964702-41c01c72-56c5-11e8-9bbd-d702e8359678.png)
1. Share the target folder to the Service Account with "edit" access, and copy the folder id
![image](https://user-images.githubusercontent.com/4360663/39964742-a897a7a2-56c6-11e8-9383-78a1097f6dde.png)
1. Replace `{parent_folder_id_here}` of [.circleci/config.yml](.circleci/config.yml#L35) with the copied folder id

## Result example

![image](https://user-images.githubusercontent.com/4360663/39965064-ed33f52c-56cc-11e8-9674-2dea95dd1b33.png)

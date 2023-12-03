

# Piggy Metrics

Piggy Metrics is a simple financial advisor app built to demonstrate the Microservice Architecture Pattern.

![Piggy Metrics](https://cloud.githubusercontent.com/assets/6069066/13830155/572e7552-ebe4-11e5-918f-637a49dff9a2.gif)

### Tools:
- Apache Maven
- Docker
- Helm
- GitLab CI/CD

![Picture](https://itdaily.be/wp-content/uploads/wpallimport/files/gitlab-gke-integration-image@2x-730x478.png)

### Goals:
 - Replace default version, build .jar-files with specified version use Gitlab CI, Apache Maven
 - Submit .jar-files and Dockerfiles to build in Google Cloud Build use Gitlab CI and cloudbuild.yaml. Store this artifacts in gcr.io
 - Deploying application use Helm.

 ____

# Actions:

### ___Application build___

For build our application - we're use .gitlab_ci.yaml file.

it includes:
###### ___**MR**:___
When merging the changed state of the code with MR - using Apache Maven, a test assembly of jar files occurs.

###### ___**Master**:___
Later, when merging with the master branch, using Apache Maven, the current version of the application is set in the format **“1.0.0-SNAPSHOT-$BUILD_TIMESTAMP-$CI_COMMIT_SHORT_SHA”**, after which service jar files are collected and along with Dockerfiles submitted for building in Google Cloud Build. Artifacts are saved in gcr.io along the path ```gcr/piggymetrics/snapshots/{service-name}:tag```

###### ___**Release**:___
Based on the results of the master job, the release job is triggered. A release branch is created here and the current state is sent to it. After which service jar files are collected and along with Dockerfiles submitted for building in Google Cloud Build. Artifacts are saved in gcr.io along the path ```gcr/piggymetrics/{service-name}:tag```

###### ___**Update version in the Master**:___
When the initial version of the application is separated into a release branch, the version is updated in the master branch for further development. The current state of the application is stored in the release branch.
This process takes place only if the job to create a release branch is completed, after saving the current state, so that we can be sure that the current state will remain intact.

At the same time, we will save the .env file that stores the updated version, which implies a condition for executing the release job, which will not be executed if the version in the master is updated. With further changes, this file will change automatically and stop unnecessary jobs.

###### ___**Random branch**:___
We also provided for changes in a random branch that is different from master and release. There will also be a build application with the current version. Artifacts are saved in gcr.io along the path ```gcr/piggymetrics/{brunch-name}/{service-name}:tag```

### ___Application deployment___

For deploying application in kubernetes we have prepared helm chart which consists of deployment/statefulset, service etc.

Helm chart is parametrised.
We need to specify each service values.yaml. Like image, service name, ports, environment variables.

To deploy application:

Switch context to the target kubernetes cluster
```helm install piggymetrics -f {servicename}-values.yaml```

___Note: CD pipeline for automated deployment is in progress.___


This repository is a clone of the [PiggyMetrics](https://github.com/sqshq/piggymetrics.git) repository.

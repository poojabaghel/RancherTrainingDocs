## Rancher Pipeline
A pipeline is a software delivery process that is broken into different stages and steps. Setting up a pipeline can help developers deliver new software as quickly and efficiently as possible. Within Rancher, you can configure pipelines for each of your Rancher projects.

Typically, pipeline stages include:

# Build:

Each time code is checked into your repository, the pipeline automatically clones the repo and builds a new iteration of your software. Throughout this process, the software is typically reviewed by automated tests.

# Publish:

After the build is completed, either a Docker image is built and published to a Docker registry or a catalog template is published.

# Deploy:

After the artifacts are published, you would release your application so users could start using the updated product.

Only administrators, cluster owners or members, or project owners can configure version control providers and manage global pipeline execution settings. Project members can only configure repositories and pipelines.

# Overviewlink

Rancher’s pipeline provides a simple CI/CD experience. Use it to automatically checkout code, run builds or scripts, publish Docker images or catalog applications, and deploy the updated software to users.

After enabling the ability to use pipelines in a project, you can configure multiple pipelines in each project. Each pipeline is unique and can be configured independently.

A pipeline is configured off of a group of files that are checked into source code repositories. Users can configure their pipelines either through the Rancher UI or by adding a .rancher-pipeline.yml into the repository.

# NOTE:
Rancher’s pipeline provides a simple CI/CD experience, but it does not offer the full power and flexibility of and is not a replacement of enterprise-grade Jenkins or other CI tools your team uses.




# Pipeline Configuration
Now that repositories are added to your project, you can start configuring the pipeline by adding automated stages and steps. For your convenience, there are multiple built-in step types for dedicated tasks.

From the Global view, navigate to the project that you want to configure pipelines.

Select Workloads in the navigation bar and then select the Pipelines tab.

Find the repository that you want to set up a pipeline for. Pipelines can be configured either through the UI or using a yaml file in the repository, i.e. .rancher-pipeline.yml or .rancher-pipeline.yaml. Throughout the next couple of steps, we’ll provide the options of how to do pipeline configuration through the UI or the YAML file.

If you are going to use the UI, select the vertical Ellipsis (…) > Edit Config to configure the pipeline using the UI. After the pipeline is configured, you must view the YAML file and push it to the repository.
If you are going to use the YAML file, select the vertical **Ellipsis (…) View/Edit YAML to configure the pipeline. If you choose to use a YAML file, you need to push it to the repository after any changes in order for it to be updated in the repository.

NOTE:
When editing the pipeline configuration, it takes a few moments for Rancher to check for an existing pipeline configuration.

Select which branch to use from the list of branches.

# Pipeline configuration is split into stages and steps. Remember that stages must fully complete before moving onto the next stage, but steps in a stage run concurrently.

Note: Pipeline configuration is split into stages and steps. Remember that stages must fully complete before moving onto the next stage, but steps in a stage run concurrently.

For each stage, you can add different step types. Learn more about how to configure each step type:

1. Run Script
2. Build and Publish Images
3. Publish Catalog Template
4. Deploy YAML
5. Deploy Catalog App
NOTE:
As you build out each step, there are different advanced options based on the step type.

# Pipeline Variable Substitution Reference
For your convenience, the following variables are available for your pipeline configuration scripts. During pipeline executions, these variables are replaced by metadata. You can reference them in the form of ${VAR_NAME}.

VARIABLE NAME	DESCRIPTION
CICD_GIT_REPO_NAME	Repository name (Github organization omitted).
CICD_GIT_URL	URL of the Git repository.
CICD_GIT_COMMIT	Git commit ID being executed.
CICD_GIT_BRANCH	Git branch of this event.
CICD_GIT_REF	Git reference specification of this event.
CICD_GIT_TAG	Git tag name, set on tag event.
CICD_EVENT	Event that triggered the build (push, pull_request or tag).
CICD_PIPELINE_ID	Rancher ID for the pipeline.
CICD_EXECUTION_SEQUENCE	Build number of the pipeline.
CICD_EXECUTION_ID	Combination of {CICD_PIPELINE_ID}-{CICD_EXECUTION_SEQUENCE}.
CICD_REGISTRY	Address for the Docker registry for the previous publish image step, available in the Kubernetes manifest file of a Deploy YAML step.
CICD_IMAGE	Name of the image built from the previous publish image step, available in the Kubernetes manifest file of a Deploy YAML step. It does not contain the image tag.

# Pipeline Setting
When a repository is enabled, a webhook is automatically set in the version control provider. By default, the pipeline is triggered by a push event to a repository, but you can modify the event(s) that trigger running the pipeline.

Available Events:

Push: Whenever a commit is pushed to the branch in the repository, the pipeline is triggered.
Pull Request: Whenever a pull request is made to the repository, the pipeline is triggered.
Tag: When a tag is created in the repository, the pipeline is triggered.

# Modifying the Event Triggers for the Repositorylink
From the Global view, navigate to the project that you want to modify the event trigger for the pipeline.

Select Workloads in the navigation bar and then select the Pipelines tab.

Find the repository that you want to modify the event triggers. Select the vertical Ellipsis (…) > Setting.

Select which event triggers (Push, Pull Request or Tag) you want for the repository.

Click Save.

For more Info go to this link
https://rancher.com/docs/rancher/v2.x/en/k8s-in-rancher/pipelines/
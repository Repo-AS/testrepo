::page{title="Continuous Integration and Continuous Delivery (CI/CD) Final Project"}

**Estimated duration**: 60 Minutes

<img src="https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBM-CD0215EN-SkillsNetwork/images/IDSN-logo.png" width="200">

Welcome to the **Continuous Integration and Continuous Delivery (CI/CD) Final Project** development environment. Now it\'s time to apply all that you have learned in the previous modules of this course. This lab environment will provide you with a sample application and an OpenShift Cluster, which will enable you to carry out the following objectives:

## Objectives

- Create a CI pipeline in GitHub Actions with steps for **linting** and **unit testing**.
- Use Tekton to create tasks for **linting**, **unit testing**, and **building an image**.
- Create an OpenShift CI Pipeline that uses the previously created Tekton steps.
- Add the deploy step to the OpenShift pipeline that deploys the code to the lab OpenShift cluster.

You should complete all the work in the final project in this lab environment.

::page{title="Prerequisite"}

## Important security information
Welcome to the Cloud IDE with OpenShift. This lab environment is where all of your development will take place. It has all the tools you will need, including an OpenShift cluster.

It is essential to understand that the lab environment is **ephemeral**. It only lives for a short while and then will be destroyed. Hence, you must push all changes made to your own GitHub repository to recreate it in a new lab environment, whenever required.

Also, note that this environment is shared and, therefore, not secure. You should not store personal information, usernames, passwords, or access tokens in this environment for any purpose.

## Your task
1. If you still need to generate a **GitHub Personal Access Token**, you should do so now. You will need it to push code back to your repository. It should have `repo` and `write` permissions and set to expire in `60` days. When Git prompts you for a password in the Cloud IDE environment, use your Personal Access Token instead.

1. You can recreate this environment by performing **Initialize Development Environment** each time.

1. Create a repository from the GitHub template provided for this lab in the next step.


::page{title="Create your own GitHub repository"}

You will need your repository to complete the final project. We have provided a GitHub Template to create your repository in your own GitHub account. **Do not Fork the repository as it\'s already a template**. This will avoid confusion when making Pull Requests in the future.

## Your task

1. In a browser, visit this GitHub repository:
	https://github.com/ibm-developer-skills-network/vselh-ci-cd-final-project-template

1. From the GitHub **Code** tab, use the green **Use this template** to create your repository from this template.

1. Select **Create a new repository** from the dropdown menu. On the next screen, fill out these prompts following the screenshot below:

![Use template](https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBM-CD0215EN-SkillsNetwork/images/cic-final-use-template.png "Use template")

1. Select your GitHub account from the dropdown list.

1. Name the new repository: `ci-cd-final-project`.

1. (Optional) Add a description to let people know what this repo is for.

1. Name the repository `ci-cd-final-project` only and ensure it is set to Public so it can be accessed during AI evaluation and by your peers.

1. Use the **Create repository from template** to create the repository in your GitHub account.

![create new repository from template](https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBM-CD0215EN-SkillsNetwork/images/cicd-final-create-repo.png "create new repository from template")

Note: These steps only need to be done once. Whenever you re-enter this lab, you should start from the next page, **Initialize Development Environment**


::page{title="Initialize Development Environment"}

As previously covered, the Cloud IDE with OpenShift environment is ephemeral, and may delete at any time. The Cloud IDE with OpenShift environment will create a new environemnt the next time you enter the lab.  Unfortunately, you will need to initialize your development environment every time. This shouldn\'t happen too often as the environment can last for several days at a time, but when it is gone, this is the procedure to recreate it.

## Overview

Each time you need to set up your lab development environment, you will need to run three commands.

Each command will be explained in further detail, one at a time, in the following section.

 **`{your_github_account}` represents your GitHub account username.**

The commands include:

```
git clone https://github.com/{your_github_account}/ci-cd-final-project.git
cd ci-cd-final-project
bash ./bin/setup.sh
exit
```

Now, let's  discuss these commands and explain what needs to be done.

## Task details

Initialize your environment using the following steps:

1. Open a terminal with `Terminal` -> `New Terminal` if one isn\'t open already.

1. Next, use the `export GITHUB_ACCOUNT=` command to export an environment variable containing your GitHub account.
> Note: Substitute your real GitHub account that you used to create the repository for the `{your_github_account}` placeholder below:

	```text
	export GITHUB_ACCOUNT={your_github_account}
	```

1. Then use the following commands to clone your repository, change it into the `devops-capstone-project` directory, and execute the `./bin/setup.sh` command.

	```bash
	git clone https://github.com/$GITHUB_ACCOUNT/ci-cd-final-project.git
	cd ci-cd-final-project
	bash ./bin/setup.sh
	```

	You should see the following at the end of the setup execution:

	![Finish setting up the terminal](https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBM-CD0215EN-SkillsNetwork/images/cid-final-terminal-finish.png "Finish setting up the terminal")

1. Finally, close the current terminal using the `exit` command. The environment won\'t be fully active until you open a new terminal in the next step.

	```bash
	exit
	```

## Validate

In order to validate that your environment is working correctly, you must open a new terminal because the Python virtual environment will only activate when a new terminal is present. You should have ended the previous task using the `exit` command to exit the terminal.

1. Open a terminal with `Terminal` -> `New Terminal` and check that everything worked correctly by using the `which python` command:

	Your prompt should look like this:

	![New terminal](https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBM-CD0215EN-SkillsNetwork/images/cicd-final-terminal-check.png "New terminal")

	Check which Python you are using:
	```bash
	which python
	```

	You should get back:

	![Which Python](https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBM-CD0215EN-SkillsNetwork/images/cicd-final-terminal-which-python.png "Which Python")

	Check the Python version:
	```bash
	python --version
	```

	You should get back some patch level of Python 3.8:

	![Python Version](https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBM-CD0215EN-SkillsNetwork/images/cicd-final-terminal-python-version.png "Python Version")

This completes the setup of the development environment.

You are now ready to start working.


::page{title="Final project scenario"}

You're part of a team responsible for building an innovative microservice, a RESTful API that allows users to manage and track counters. Another team has already developed the user interface (UI) for this microservice, and it\'s now your turn to ensure the reliability and efficiency of the backend services.

**Continuous Integration (CI) with GitHub Actions**
Your first task is to set up CI pipelines using GitHub Actions. The codebase comes with unit tests for the provided endpoints. Your goal is to automate the linting and testing processes. You will create a GitHub Actions workflow that triggers whenever changes are pushed to the repository.

**Continuous Deployment (CD) with OpenShift Pipelines**
In the second phase, establish CD pipelines within OpenShift Pipelines. These pipelines should include linting, testing, building an image, and the seamlessly deploying the microservice to an OpenShift cluster.

You need to provide the URL for your repository with the GitHub workflow and tekton yaml files in addition to other terminal outputs and screenshots as evidence of your work. Your evidence will be essential for either peer project evaluation or AI graded evaluation. Best of luck with your project!

::page{title="Final Project"}

###  Note:

1. Please ensure that all updates to the files are properly saved.

2. Save and Push your project files to Github and capture screenshots as mentioned in the respective tasks.

3. You can submit your project deliverables through either Option 1: AI-Graded Submission and Evaluation or Option 2: Peer-Graded Submission and Evaluation.

4. **For Option 1: AI-Graded Submission and Evaluation:**  
   - Submission requires the Github URL of **workflow.yaml**, **tasks.yaml**, and **Readme.md** files along with Text response for **Task 7 and Task 10** and screenshots for **Task 6**, **Task 8** and **Task 9**.

5. **For Option 2: Peer-Graded Submission and Evaluation:**  
   - Submission requires screenshots for **Tasks 6 to 10** along with Github URL of **workflow.yaml**, **tasks.yaml** files and **Github repo** URL also.

##  Exercise 0 - Push CI code to GitHub

To test the workflow and the CI pipeline, you need to commit the changes and push your branch back to the GitHub repository. Each new push to the main branch should trigger the workflow.

## Your task

1. Configure the Git account with your email and name using the `git config --global user.email` and `git config --global user.name` commands.

	<details>
		<summary>Click here for a hint.</summary>

	Open the terminal and configure your email:
	```
	git config --global user.email "you@example.com"
	```

	Open the terminal and configure your user name
	```
	git config --global user.name "Your Name"
	```

	</details>

2. Update your Readme.md file in your GitHub repository and add the Project name as `ci-cd-final-project` under **CI/CD Tools and Practices Final Project Template**.

3. Make sure to stage all the changes you made in the exercises and push them to your forked repo on GitHub.

	<details>
		<summary>Click here for a hint.</summary>

	You can use the following commands to commit your changes to staging and then them push to your forked repository:
	```shell
	git add -A
	git commit -m "COMMIT MESSAGE"
	git push
	```
	</details>



Your output should look similar to the image below:

### Solution
![CICD GitHub commit](https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBM-CD0215EN-SkillsNetwork/images/cicd-github-commit.png "CICD GitHub commit")

**Assessment**: 

**For Option 1 - AI Graded Submission and Evaluation**: Copy and paste the the public Github URL of `Readme.md` file and save it for the Submission later.

**For Option 2 - Peer Graded Submission and Evaluation**: Copy and paste the the public Github URL of `ci-cd-final-project` and save it for the Peer review Submission later.

::page{title="Exercise 1: Create basic workflow"}

Your GitHub repository has an empty workflow file, `.github/workflows/workflow.yml.` You will create the CI workflow by writing several steps in this workflow file.

::openFile{path="/home/project/ci-cd-final-project/.github/workflows/workflow.yml"}

## Your task

Open the `.github/workflows/workflow.yml` file and add the following:
1. name: `CI workflow`
1. workflow triggers: `push on main branch` and `pull_request on main branch`
1. Jobs
	- runs-on: `ubuntu-latest`
	- container: `python:3.9-slim`
1. Checkout step:
	- name: `Checkout`
	- uses: `actions/checkout@v3`
1. Install Dependencies step:
	- name: `Install dependencies`
	- run `python -m pip install --upgrade pip` and `pip install -r requirements.txt` commands

You can also refer to the videos and labs in the module 2 of the course in case you want to familiarize yourself with the concepts before proceeding further.


### Hint

<details>
<summary>Click here for a hint.</summary>

You can use the following file as a template for this exercise:
```
name: {name of workflow}

on:
  push:
    branches: {array of branches}
  pull_request:
    branches: {array of branches}

jobs:
  build:
    runs-on: {placeholder}
    container: {placeholder}
    steps:
      - name: {placeholder}
        uses: {placeholder}
	  - name: {placeholder}
		run: |
		{first command}
		{second command}
```
</details>

::page{title="Exercise 2: Add the linting step to CI workflow"}

Next, you will add the `Lint` step to the GitHub workflow. You will use `Flake8` module for linting. Open the `.github/workflows/workflow.yml` file and complete the following tasks.

::openFile{path="/home/project/ci-cd-final-project/.github/workflows/workflow.yml"}

## Your task
Add a linting task with the following details:
1. name: `Lint with flake8`
1. commands:
	- `flake8 service --count --select=E9,F63,F7,F82 --show-source --statistics`
	- `flake8 service --count --max-complexity=10 --max-line-length=127 --statistics`

You can refer to the videos and labs in the module 2 for help.

### Hint

<details>
<summary>Click here for a hint.</summary>

You can use the following file as a template for this exercise:
```
	- name: {placeholder}
	run: |
	  {first command}
	  {second command}
```
</details>

::page{title="Exercise 3: Add the test step to CI workflow"}

Next, you will add the `Test` step to the GitHub workflow. You will use the `Nose` module for running the tests. Open the `.github/workflows/workflow.yml` file and complete the following tasks.

::openFile{path="/home/project/ci-cd-final-project/.github/workflows/workflow.yml"}

## Your task
Add a test step with the following details:
1. name: `Run unit tests with nose`
1. command:
	- `nosetests -v --with-spec --spec-color --with-coverage --cover-package=app`

You can refer to the videos and labs in the module 2 for help.

### Hint

<details>
<summary>Click here for a hint.</summary>

You can use the following file as a template for this exercise:
```
  - name: Run unit tests with nose
    run: {insert command here}
```
</details>

> Make sure to stage all the changes you made in the exercises and push them to your forked repo on GitHub.

**Assessment**: 

**For Option 1 - AI Graded Submission and Evaluation** and **For Option 2 - Peer Graded Submission and Evaluation**: Copy and paste the the public Github URL of `workflow.yaml` and save it in a text file named `.github/workflows/workflow.yml` for the Submission later.

::page{title="Exercise 4: Validate GitHub Actions Workflow"}

1. To validate that your workflow ran and was successful, simply go to your version of the repository on GitHub and click on Actions.

![Open GitHub Actions](https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBM-CD0215EN-SkillsNetwork/images/cicd-github-validate-1.png "Open GitHub Actions")

You can click on the `CI Workflow` to see more details.

![See GitHub action details](https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBM-CD0215EN-SkillsNetwork/images/cicd-github-validate-2.png "See GitHub action details")

2. Finally, you can drill into the action to confirm all the steps succeeded.


<img src="https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/1Lhp_gKVHqQDje__rcl5Lg/cicd-github-validate-3-sample.png" >

**Assessment**: 

**For Option 2 Peer Graded Submission and Evaluation**: Take a screenshot of the action workflow page and name the file `cicd-github-validate(.png)` and save it for the Peer review submission later.

3. To get the list of the action workflow of your GitHub repository in the terminal, Run the following command:-

	```shell
	gh run list
	gh run view <run-id>
	gh run view <run-id> verbose
	```
	*Replace <run-id> with the ID displayed in the output from the gh run list command.*
Note: Ensure you are inside the correct repository directory and have successfully authenticated using ```gh auth login``` before running these commands.

Your output should appear similar to the image below:

![action workflow python.png](https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/1iBDcLSx1EStR_HYMUMPwg/action%20workflow%20python.png)

**Assessment**: 

**For Option 1 - AI Graded Submission and Evaluation**: Copy and paste the the terminal output of `action workflow` in the text file named `cicd-github-validate` and save it for the Submission later.


::page{title="Exercise 5: Create cleanup Tekton task"}

Congratulations on successfully creating the GitHub CI workflow to checkout, lint, and test your code. The next step is to create the CD workflow in OpenShift. Before you can do that, create the cleanup task that will clean the output workspace so that the CD pipeline can start fresh.

Open the `.tekton/tasks.yml` file and complete the following tasks.

::openFile{path="/home/project/ci-cd-final-project/.tekton/tasks.yml"}

## Your task
Add a cleanup task with the following details:
1. apiVersion: `tekton.dev/v1beta1`
1. kind: `Task`
1. name: `cleanup`
1. spec.workspaces.name: `source`

This task will have a single step called `remove` as follows:
1. name: `remove`
1. image: `alpine:3`
1. env:
	- name: `WORKSPACE_SOURCE_PATH`
	- value: `$(workspaces.source.path)`
1. workingDir: `$(workspaces.source.path)`
1. securityContext
	- runAsNonRoot: `false`
	- runAsUser: `0`
1. script:
	```
	#!/usr/bin/env sh
        set -eu
        echo "Removing all files from ${WORKSPACE_SOURCE_PATH} ..."
        # Delete any existing contents of the directory if it exists.
        #
        # We don't just "rm -rf ${WORKSPACE_SOURCE_PATH}" because ${WORKSPACE_SOURCE_PATH} might be "/"
        # or the root of a mounted volume.
        if [ -d "${WORKSPACE_SOURCE_PATH}" ] ; then
          # Delete non-hidden files and directories
          rm -rf "${WORKSPACE_SOURCE_PATH:?}"/*
          # Delete files and directories starting with . but excluding ..
          rm -rf "${WORKSPACE_SOURCE_PATH}"/.[!.]*
          # Delete files and directories starting with .. plus any other character
          rm -rf "${WORKSPACE_SOURCE_PATH}"/..?*
        fi
	```

You can also refer to the videos and labs in the module 3 of the course in case you want to familiarize yourself with the concepts before proceeding further.

### Hint

<details>
<summary>Click here for a hint.</summary>

You can use the following file as a template for this exercise:
```
---
apiVersion: {placeholder}
kind: {placeholder}
metadata:
  name: {placeholder}
spec:
  description: This task will clean up a workspace by deleting all the files.
  workspaces:
    - name: {placeholder}
  steps:
    - name: {placeholder}
      image: {placeholder}
      env:
        - name: {placeholder}
          value: {placeholder}
      workingDir: {placeholder}
      securityContext:
        runAsNonRoot: {placeholder}
        runAsUser: {placeholder}
      script: |
        {placeholder}
```
</details>

::page{title="Exercise 6: Create test Tekton task"}

You have added the `cleanup` task to the tekton file. Next, add the test task called `nose` right under the `cleanup` task.

Open the `.tekton/tasks.yml` file and complete the following tasks.

::openFile{path="/home/project/ci-cd-final-project/.tekton/tasks.yml"}

## Your Task
Add a testing task with the following details:
1. apiVersion: `tekton.dev/v1beta1`
1. kind: `Task`
1. name: `nose`
1. spec.workspaces.name: `source`
1. params:
    - name: `args`
    - description: `Arguments to pass to nose`
    - type: `string`
    - default: `"-v"`

This task will have a single step called `nosetests` as follows:
1. name: `nosetests`
1. image: `python:3.9-slim`
1. workingDir: `$(workspaces.source.path)`
1. script:
	```
	  #!/bin/bash
	  set -e
	  python -m pip install --upgrade pip wheel
	  pip install -r requirements.txt
	  nosetests $(params.args)
	```

You can also refer to the videos and labs in the module 3 of the course in case you want to familiarize yourself with the concepts before proceeding further.

### Hint

<details>
<summary>Click here for a hint.</summary>

You can use the following file as a template for this exercise:
```
---
apiVersion: {placeholder}
kind: {placeholder}
metadata:
  name: {placeholder}
spec:
  workspaces:
    - name: {placeholder}
  params:
    - name: {placeholder}
      description: {placeholder}
      type: {placeholder}
      default: {placeholder}
  steps:
    - name: {placeholder}
      image: {placeholder}
      workingDir: {placeholder}
      script: |
        {placeholder}
```
</details>

> Make sure to stage all the changes you made in the exercises and push them to your forked repo on GitHub.

**Assessment**: 

**For Option 1 - AI Graded Submission and Evaluation** and **For Option 2 - Peer Graded Submission and Evaluation**: Copy and paste the the public Github URL of `.tekton/tasks.yml` and save it for the Submission later.

::page{title="Exercise 7: Create OpenShift pipeline"}

You are almost done with the final project. Now that you have the tasks created, you will need to:
- Install the tasks in the lab OpenShift cluster
- Create CD pipeline

**Please follow the porcess mentioned in the Hands-on Lab: CI/CD with OpenShift in Module 4 Pipelines for doing the below tasks.**

You can refer to the videos and other content in the Module 4 [ Hands-on Lab: CI/CD with OpenShift](https://www.coursera.org/learn/continuous-integration-and-continuous-delivery-ci-cd/ungradedLti/To2af/hands-on-lab-ci-cd-with-openshift-pipelines " Hands-on Lab: CI/CD with OpenShift") of the course in case you want to familiarize yourself with the concepts before proceeding further.

## Your task
1. In the terminal, install the `cleanup` and `nose` tasks by applying the `tasks.yml` file with `kubectl apply -f .tekton/tasks.yml` command.
1. Open the OpenShift console from the lab environment.
1. Create a PVC through terminal as mentioned in the previous lab or either from the `Administrator` perspective with
	- storageclass: `skills-network-learner`
	- select a PVC: `oc-lab-pvc`
	- size: 1GB
1. Create a new pipeline and a workspace called `output`
1. Add the following steps in this order:
	- cleanup
	- git clone
	- flake8 linting
	- nose tests
	- buildah task
1. Test the pipeline works. Take a screenshot as described in this exercise\'s `Solutions` section.
1. Add the final step of deploying the application to the lab openshift cluster using the `OpenShift client` task and the `oc deploy command`.
	- `oc create deployment $(params.app-name) --image=$(params.build-image) --dry-run=client -o yaml | oc apply -f -`


You can refer to the videos and other content in the module 4 of the course in case you want to familiarize yourself with the concepts before proceeding further.

### Hint
The PVC opions should look as follows:
<img src="https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/jzI2x8ntDsYVFiLpXPU5BA/oc-pipelines-console-pvc-details-sample%20-1-.png">

**For Option 1 - AI Graded Submission and Evaluation** and **For Option 2 - Peer Graded Submission and Evaluation**: Take a screenshot of this page and save it as `oc-pipelines-console-pvc-details(.png)` for the submission later.

At the end of this exercise, you can validate the solution as follows:

### Solution
1. Confirm the pipeline has the following steps:

	<img src="https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/Naw7xQiFeGwWIXQ5Sn8ebw/oc-pipelines-oc-final-sample%201%20-1-.png" >

**Assessment**:

**For Option 1 - AI Graded Submission and Evaluation** and **For Option 2 - Peer Graded Submission and Evaluation**: Take a screenshot of this page and save it as `oc-pipelines-oc-final(.png)` for the submission later.

2. Confirm the pipeline runs as shown:

	<img src="https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/EzjHsI90JSl3nu_eWb8NYw/oc-pipelines-oc-green-sample%20-1-.png">

**Assessment**: 

**For Option 1 - AI Graded Submission and Evaluation** and **For Option 2 - Peer Graded Submission and Evaluation**: Take a screenshot of this page and save it as `oc-pipelines-oc-green(.png)` for the submission later.

3. Confirm you can see the application logs in the OpenShift console:

	<img src="https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/w4sVXmeTusp02Im2HOaxyg/oc-pipelines-app-logs-sample%20-1-.png"  width="" height="">

**Assessment**: 

**For Option 1 - AI Graded Submission and Evaluation**: Copy and paste the the output of SERVICERUNNING and save it in a text file  named as `oc-pipeline-app-logs` for the Final Project Submission and Evaluation.

**For Option 2 - Peer Graded Submission and Evaluation**: Take a screenshot of the `SERVICERUNNING` and save it as `oc-pipeline-app-logs.png` for Peer Assignment.

::page{title="Submission"}

## Commit the code to your Github repository

1. Use `git status` to ensure that you have committed your changes locally in the development environment.

1. Use the `git add` command to update the staging area\'s code.

1. Commit your changes using `git commit -m <commit message>`

1. Push your local changes to a remote branch using the `git push` command

	> Note: Use your GitHub **Personal Access Token** as your password in the Cloud IDE environment. You may also need to configure Git the first time you use it with:
	```text
	git config --local user.email "you@example.com"
	git config --local user.name "Your Name"
	```

Submit the link to your GitHub repository when completed.


::page{title="Evaluation"}

Follow the checklist below to verify that your project meets all requirements before submission.

**Submit your work through either Option 1: AI-Graded Submission and Evaluation or Option 2: Peer-Graded Submission and Evaluation, depending on the submission path you choose for project evaluation.**

### Option 1: AI-Graded Submission

1. Submit the GITHUB URL of the `README.md file` that contains the Project name details. (2 points)
2. Provide the GitHub URL of `.github/workflows/workflow.yml` showing the code snippet for the Lint with flake8 step or ESlint and the code snippet for the Run unit tests with nose step or Jest-test(4 points)
3. Provide the GitHub URL of `.tekton/tasks.yml` showing the code snippet for the cleanup task and the code snippet for the nose task or Jest-test(4 points)
4. Provide the screenshot of the OpenShift PersistentVolumeClaim details in a file named `oc-pipelines-console-pvc-details.png`(2 points)
5. Provide the text of terminal output named `cicd-github-validate(.png)`showing details of GitHub actions running successfully in the actions workflow containing all the steps.(2 points)
6. Provide the screenshot showing details of the OpenShift Pipeline `oc-pipelines-oc-final.png`(2 points)
7. Provide the screenshot showing details of the OpenShift Pipeline running successfully in a file named `oc-pipelines-oc-green.png`(2 points)
8. Provide the text response showing details of the OpenShift application logs(2 points)

### Option 2: Peer-Graded Submission
1. The GitHub repo URL that you pushed your changes to. Should be of the format https://github.com/{your_github_account}/ci-cd-final-project.git
2. Provide the GitHub URL of the `.github/workflows/workflow.yml` file showing the code snippet for the linting step.
3. Provide the GitHub URL of the `.github/workflows/workflow.yml` file showing the code snippet for the test step.
4. Provide the GitHub URL of the `.tekton/tasks.yml` file showing the code snippet for the cleanup task.
5. Provide the GitHub URL of the `.tekton/tasks.yml` file showing the code snippet for the nose test task.
6. Screenshot showing OpenShift PVC details. Name this file `oc-pipelines-console-pvc-details(.png)`
7. Screenshot showing GitHub actions running successfully. Name this file `cicd-github-validate(.png)`
8. Screenshot showing details of the OpenShift Pipeline. Name this file `oc-pipelines-oc-final(.png)`
9. Screenshot showing details of the OpenShift Pipeline running successfully. Name this file `oc-pipelines-oc-green(.png)`
10. Screenshot of the running application logs from OpenShift console. Name this file `oc-pipelines-app-logs(.png)`
## Sample Files for Tasks 6-10

<details>

<summary>Click here for a hint.</summary>

1. Task 6: `oc-pipelines-console-pvc-details(.png/jpg)`

	<img src="https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/jzI2x8ntDsYVFiLpXPU5BA/oc-pipelines-console-pvc-details-sample%20-1-.png">

2. Task 7: `cicd-github-validate(.png/jpg)`

	<img src="https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/DddtQjn5WcqWyhiuHp9TnA/cicd-github-validate-3-sample%20-1-.png">


2. Task 8: `oc-pipelines-oc-final(.png/jpg)`

	<img src="https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/Naw7xQiFeGwWIXQ5Sn8ebw/oc-pipelines-oc-final-sample%201%20-1-.png">

3. Task 9: `oc-pipelines-oc-green(.png/jpg)`

	<img src="https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/EzjHsI90JSl3nu_eWb8NYw/oc-pipelines-oc-green-sample%20-1-.png" >)

5. Task 10: `oc-pipelines-app-logs(.png/jpg)`

	<img src="https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/w4sVXmeTusp02Im2HOaxyg/oc-pipelines-app-logs-sample%20-1-.png">
</details>

::page{title="Conclusion"}

Congratulations on completing the CI/CD Final Project. Now you understand how to create continuous integration and continous deployment pipelines with best practices in mind.

## Next Steps

Incorporate these new practices into your projects at home and work. Write the test cases for the code you "wish you had,"then write the code to make those tests pass. Describe the behavior of your system from the outside in and then prove that it behaves that way by automating those tests with Behave.

## Author(s)

Skills Networks
<!---
## Changelog

| Date | Version | Changed by | Change Description |
|------|--------|--------|---------|
| 2023-09-04 | 0.1 | UL | Initial version created |
| 2023-09-20| 0.2 | Anita Narain | ID Reviewed |
| 2023-09-21| 0.3 | Mary Stenberg | QA Reviewed with edits |
| 2023-10-09 | 0.4 | K Sundararajan | Updates done based on Beta testing |
| 2025-05-05 | 0.5 | Manvi Gupta | updated Screenshots |
--->

## <h3 align="center"> &#169; IBM Corporation 2024. All rights reserved. <h3/>
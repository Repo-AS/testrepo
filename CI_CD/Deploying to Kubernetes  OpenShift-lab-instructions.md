::page{title="Deploying to Kubernetes / OpenShift"}

<img src="https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBM-CD0215EN-SkillsNetwork/images/IDSN-logo.png" width="200" />

**Estimated time needed:** 20 minutes

Welcome to the hands-on lab for **Deploying to Kubernetes / OpenShift**. You are now at the deploy step, which is the last step in your CD pipeline. For this step, you will use the OpenShift client to deploy your Docker image to an OpenShift cluster.

> Note: OpenShift is based on Kubernetes. Anything you can do with Kubernetes, you can do that and more with OpenShift. This lab uses the commands `kubectl` and `oc` interchangeably because `oc` is a proper superset of `kubectl`.

## Learning Objectives

After completing this lab, you will be able to:

-   Determine if the openshift-client ClusterTask is available on your cluster
    
-   Describe the parameters required to use the openshift-client ClusterTask
    
-   Use the openshift-client ClusterTask in a Tekton pipeline to deploy your Docker image to Kubernetes
    
-   Deploying to Kubernetes is straightforward — keeping it performant and cost-efficient at scale is the hard part. IBM Turbonomic uses AI to continuously analyze your Kubernetes deployments and automate resource decisions, ensuring every container gets what it needs without over-provisioning your cluster. Get started with a free trial at [ibm.biz/snp-turbo.](https://ibm.biz/snp-turbo)
    

::page{title="Set Up the Lab Environment"}

You have a little preparation to do before you can start the lab.

## Open a Terminal

Open a terminal window by using the menu in the editor: Terminal > New Terminal.

![Terminal](https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBM-CD0215EN-SkillsNetwork/images/01_terminal.png "New Terminal option on the Terminal menu")

In the terminal, if you are not already in the `/home/project` folder, change to your project folder now.

```bash
cd /home/project

```

## Clone the Code Repo

Now, get the code that you need to test. To do this, use the `g&#8203;it clone` command to clone the Git repository:

```bash
git clone https://github.com/ibm-developer-skills-network/wtecc-CICD_PracticeCode.git

```

Your output should look similar to the image below:

![Git Clone](https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBM-CD0215EN-SkillsNetwork/images/01_git_clone_code.png "Cloned repo output")

## Change to the Labs Directory

Once you have cloned the repository, change to the labs directory.

```bash
cd wtecc-CICD_PracticeCode/labs/06_deploy_to_kubernetes/

```

You are now ready to start the lab.

### Optional

If working in the terminal becomes difficult because the command prompt is very long, you can shorten the prompt using the following command:

```bash
export PS1="[\[\033[01;32m\]\u\[\033[00m\]: \[\033[01;34m\]\W\[\033[00m\]]\$ "

```

* * *

::page{title="Prerequisites"}

If you did not compete the previous labs, you will need to run the following commands to catch up and prepare your environment for this lab. If you have completed the previous labs, you may skip this step, although repeating it will not harm anything because Kubernetes is declarative and idempotent. It will always put the system in the same state given the same commands.

Issue the following commands from the `/home/project/wtecc-CICD_PracticeCode/labs/06_deploy_to_kubernetes/` folder to install everything from the previous labs.

```bash
cd /home/project/wtecc-CICD_PracticeCode/labs/06_deploy_to_kubernetes/

```

The `git-clone` task is part of the **Tekton Catalog** and is indexed on **Artifact Hub** for discovery. You can install the task using either of the following options.

**Option 1: Discover via Artifact Hub and apply the raw manifest**

```bash
kubectl apply -f https://github.com/tektoncd/catalog/raw/main/task/git-clone/0.10/git-clone.yaml

```

**Option 2: Install directly from the Tekton Catalog**

Artifact Hub indexes tasks from the official Tekton Catalog hosted on GitHub. You can install the same task directly from the source repository:

```bash
kubectl apply -f https://raw.githubusercontent.com/tektoncd/catalog/main/task/git-clone/0.9/git-clone.yaml

```

Both options install the git-clone task into your cluster under the currently active namespace.

**Verify the installation**

After installation, confirm that the task is available:

```bash
kubectl get task git-clone

```

You should see the git-clone task listed in the output.

```bash
kubectl apply -f tasks.yaml
kubectl apply -f pvc.yaml

```

Check that you have all of the previous tasks installed:

```bash
tkn task ls

```

You should see:

```txt
NAME               DESCRIPTION              AGE
cleanup            This task will clean...  2 minutes ago
git-clone          These Tasks are Git...   2 minutes ago
flake8             This task will run ...   1 minute ago
echo                                        46 seconds ago
nose                                        46 seconds ago

```

You are now ready to continue with this lab.

* * *

::page{title="Step 1: Check for the openshift-client ClusterTask"}

Your pipeline currently has a placeholder for a `deploy` step that uses the `e&#8203;cho` task. Now it is time to replace it with a real deployment.

Instead of installing it yourself, you first check the ClusterTasks in your cluster to see if it already exists. Luckily, the OpenShift environment you are using already has `openshift-client` installed as a **ClusterTask**. A ClusterTask is installed cluster-wide by an administrator and anyone can use it in their pipelines without having to install it themselves.

Check that the `openshift-client` task is installed as a ClusterTask using the command kubectl get clustertasks.

* * *

::page{title="Step 2: Reference the openshift-client task"}

First you need to update the `pipeline.yaml` file to use the new `openshift-client` task.

Open `pipeline.yaml` in the editor and scroll down to the `deploy` pipeline task. To open the editor, click the button below.

&nbsp;

::openFile{path="/home/project/wtecc-CICD_PracticeCode/labs/06_deploy_to_kubernetes/pipeline.yaml"}

You must now reference the new `openshift-client` ClusterTask that you want to use in the `deploy` pipeline task.

In the previous steps, you simply changed the name of the reference to the task, but since the `openshift-client` task is installed as a **ClusterTask**, you need to add the statement `kind: ClusterTask` under the name so that Tekton knows to look for a **ClusterTask** and not a regular **Task**.

### Your Task

Change the `taskRef` from `e&#8203;cho` to `openshift-client` and add a line below it with `kind: ClusterTask` to indicate that this is a ClusterTask:

### Hint

<details>
<summary>Click here for a hint.</summary>
<blockquote><p>You want to change this name and add <code>kind:</code> below it.</p></blockquote><pre><code class="language-yaml">      taskRef:
        name: echo
</code></pre>
</details>

### Solution

<details>
<summary>Click here for the answer.</summary>
<pre><code class="language-yaml">      taskRef:
        name: openshift-client
		kind: ClusterTask
</code></pre>
</details>

::page{title="Step 3: Update the Task Parameters"}

The documentation for the `openshift-client` task details that there is a parameter named `SCRIPT`that you can use to run `oc` commands. Any command you can use with `kubectl` can also be used with `oc`. This is what you will use to deploy your image.

The command to deploy an image on OpenShift is:

```
oc create deployment {name} --image={image-name}

```

Since you might want to reuse this pipeline to deploy different applications, you should make the deployment name a parameter that can be passed in when the pipeline runs. You already have the image name as a parameter from the build task that you can use.

### Your Task

Change the `message` parameter to `SCRIPT` and specify the value of `"oc create deploy $(params.app-name) --image=$(params.build-image)"` in quotes.

### Hint

<details>
<summary>Click here for a hint.</summary>
<blockquote><p>You want to change the name and value of the message parameter.</p></blockquote><pre><code class="language-yaml">      params:
      - name: message
        value: "Deploying $(params.branch) branch of $(params.repo-url) ..."
</code></pre>
</details>

### Solution

<details>
<summary>Click here for the answer.</summary>
<pre><code class="language-yaml">      params:
      - name: SCRIPT
        value: "oc create deploy $(params.app-name) --image=$(params.build-image)"
</code></pre>
</details>

* * *

::page{title="Step 4: Update the Pipeline Parameters"}

Now that you are passing in the `app-name` parameter to the `deploy` task, you need to go back to the top of the `pipeline.yaml` file and add the parameter there so that it can be passed into the pipeline when it is run.

### Your Task

Add a parameter named `app-name` to the existing list of parameters at the top of the pipeline under `spec.params`.

### Hint

<details>
<summary>Click here for a hint.</summary>
<blockquote><p>You want to add <code>app-name</code> to this parameter list.</p></blockquote><pre><code class="language-yaml">spec:
  params:
    - name: build-image
    - name: repo-url
    - name: branch
</code></pre>
</details>

### Solution

<details>
<summary>Click here for the answer.</summary>
<pre><code class="language-yaml">spec:
  params:
    - name: app-name
</code></pre>
</details>

* * *

::page{title="Step 5: Check Your work"}

## Code Check

If you changed everything correctly, the full `deploy` task in the pipeline should look like this:

```yaml
    - name: deploy
      taskRef:
        name: openshift-client
        kind: ClusterTask
      params:
      - name: SCRIPT
        value: "oc create deploy $(params.app-name) --image=$(params.build-image)"
      runAfter:
        - build

```

Also, the full parameter list for your pipeline should look like this:

```yaml
spec:
  params:
    - name: app-name
    - name: build-image
    - name: repo-url
    - name: branch
      default: master

```

Save your changes before you continue.

## Terminal Folder Check

Before you proceed with running commands in the terminal, make sure that you are in the `/home/project/wtecc-CICD_PracticeCode/labs/06_deploy_to_kubernetes/` folder.

Go to the terminal and use the `p&#8203;wd` command just to be sure.

```bash
pwd

```

You should see: `/home/project/wtecc-CICD_PracticeCode/labs/06_deploy_to_kubernetes/`. If you do not, you should `c&#8203;d` into that folder now:

```bash
cd /home/project/wtecc-CICD_PracticeCode/labs/06_deploy_to_kubernetes/

```

You are now ready to run the terminal commands in the next step.

* * *

::page{title="Step 6: Apply Changes and Run the Pipeline"}

## Apply the Pipeline

Apply the same changes you just made to `pipeline.yaml` to your cluster:

```bash
kubectl apply -f pipeline.yaml

```

## Start the Pipeline

When you start the pipeline, you now need to pass in the `app-name` parameter, which is the name of the application to deploy.

Your application is called `hitcounter` so this is the name that you will pass in, along with all the other parameters from the previous steps.

Now, start the pipeline to see your new deploy task run. Use the Tekton CLI `pipeline start` command to run the pipeline, passing in the parameters `repo-url`, `branch`, `app-name`, and `build-image` using the `-p` option. Specify the workspace `pipeline-workspace` and persistent volume claim `pipelinerun-pvc` using the `-w` option:

```bash
tkn pipeline start cd-pipeline \
    -p repo-url="https://github.com/ibm-developer-skills-network/wtecc-CICD_PracticeCode.git" \
    -p branch=main \
    -p app-name=hitcounter \
    -p build-image=image-registry.openshift-image-registry.svc:5000/$SN_ICR_NAMESPACE/tekton-lab:latest \
    -w name=pipeline-workspace,claimName=pipelinerun-pvc \
    --showlog

```

You should see `Waiting for logs to be available...` while the pipeline runs. The logs will be shown on the screen. Wait until the pipeline run completes successfully.

## Check the Run Status

You can see the pipeline run status by listing the pipeline runs with:

```bash
tkn pipelinerun ls

```

You should see:

```txt
NAME                    STARTED         DURATION     STATUS
cd-pipeline-run-fbxbx   1 minute ago    59 seconds   Succeeded

```

You can check the logs of the last run with:

```bash
tkn pipelinerun logs --last

```

If it is successful, the last line you should see in the logs is:

```
[deploy : oc] deployment.apps/hitcounter created

```

If it says anything but _created_ something has gone wrong.

* * *

::page{title="Step 7: Check the Deployment"}

Now, check to see if the deployment is running. Use the `kubectl` command to check that your deployment is in a running state.

```bash
kubectl get all -l app=hitcounter

```

You should see:

```
NAME                              READY   STATUS    RESTARTS   AGE
pod/hitcounter-7c9f95784d-rk4tf   1/1     Running   0          2m46s

NAME                         READY   UP-TO-DATE   AVAILABLE   AGE
deployment.apps/hitcounter   1/1     1            1           2m46s

NAME                                    DESIRED   CURRENT   READY   AGE
replicaset.apps/hitcounter-7c9f95784d   1         1         1       2m46s

```

If your **pod** is running, your application has been successfully deployed.

* * *

::page{title="Conclusion"}

Congratulations! You have just added the ability to deploy a Docker image to an OpenShift / Kubernetes cluster.

In this lab, you learned how to use the `openshift-client` ClusterTask from the Tekton catalog. You learned how to modify your pipeline to reference the task as a ClusterTask and configure its parameters. You also learned how to pass additional parameters to a pipeline to specify the application name, and how to run the pipeline to deploy an image to OpenShift.

## Next Steps

Try to set up a pipeline to deploy an image with Tekton from one of your own code repositories.

If you are interested in continuing to learn about Kubernetes and containers, you should get your own [free Kubernetes cluster](https://www.ibm.com/cloud/container-service/?utm_source=skills_network&utm_content=in_lab_content_link&utm_id=Lab-IBM-CD0215EN-SkillsNetwork) and your own free [IBM Container Registry](https://www.ibm.com/cloud/container-registry?utm_source=skills_network&utm_content=in_lab_content_link&utm_id=Lab-IBM-CD0215EN-SkillsNetwork).

Automate Kubernetes resource optimization from day one — try IBM Turbonomic free at [ibm.biz/snp-turbo.](https://ibm.biz/snp-turbo)

## Author(s)

[John J. Rofrano](https://www.coursera.org/instructor/johnrofrano)

!

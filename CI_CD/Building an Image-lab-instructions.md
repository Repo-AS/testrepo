::page{title="Building an Image"}

<img src="https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBM-CD0215EN-SkillsNetwork/images/IDSN-logo.png" width="200" />

**Estimated time needed:** 20 minutes

Welcome to the hands-on lab for **Building an Image**. You are now at the build step, which is the next to last step in your CD pipeline. Before you can deploy your application, you need to build a Docker image and push it to an image registry. Luckily, there is a ClusterTask from the Tekton catalog available on your cluster that can do that -- the `buildah` ClusterTask.

## Learning Objectives

After completing this lab, you will be able to:

-   Determine which ClusterTasks are available on your cluster
    
-   Describe the parameters required to use the buildah ClusterTask
    
-   Use the buildah ClusterTask in a Tekton pipeline to build an image and push it to an image registry
    
-   Understanding container images is your starting point — and as you move to running containers in production, resource management becomes essential. IBM Turbonomic uses AI to optimize the resources your containerized workloads consume, ensuring performance targets are met while eliminating overprovisioned infrastructure. Get started with a free trial at [ibm.biz/snp-turbo.](https://ibm.biz/snp-turbo)
    

::page{title="Set Up the Lab Environment"}

You have a little preparation to do before you can start the lab.

## Open a Terminal

Open a terminal window by using the menu in the editor: Terminal > New Terminal.

![Terminal](https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBM-CD0215EN-SkillsNetwork/images/01_terminal.png "New Terminal option on Terminal menu")

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
cd wtecc-CICD_PracticeCode/labs/05_build_an_image/

```

You are now ready to start the lab.

### Optional

If working in the terminal becomes difficult because the command prompt is very long, you can shorten the prompt using the following command:

```bash
export PS1="[\[\033[01;32m\]\h\[\033[00m\]: \[\033[01;34m\]\W\[\033[00m\]]\$ "

```

::page{title="Prerequisites"}

If you did not complete the previous labs, you will need to run the following commands to catch up and prepare your environment for this lab. If you have completed the previous labs, you may skip this step, although repeating it will not harm anything because Kubernetes is declarative and idempotent. It will always put the system in the same state given the same commands.

Issue the following commands to install everything from the previous labs.

You can browse the Tekton Catalog to find the `git-clone` and `flake8` task, copy the URL to the task's yaml file, and apply it manually using kubectl.

The `git-clone` and `flake8` tasks are part of the Tekton Catalog and is indexed on Artifact Hub for discovery. You can install the task using either of the following options.

**Option 1: Discover via Artifact Hub and apply the raw manifest**

```bash
kubectl apply -f https://github.com/tektoncd/catalog/raw/main/task/git-clone/0.10/git-clone.yaml

```

```bash
kubectl apply -f https://github.com/tektoncd/catalog/raw/main/task/flake8/0.1/flake8.yaml

```

**Option 2: Install directly from the Tekton Catalog**

Artifact Hub indexes tasks from the official Tekton Catalog hosted on GitHub. You can install the same task directly from the source repository:

```bash
kubectl apply -f https://raw.githubusercontent.com/tektoncd/catalog/main/task/git-clone/0.9/git-clone.yaml

```

```bash
kubectl apply -f https://raw.githubusercontent.com/tektoncd/catalog/main/task/flake8/0.1/flake8.yaml

```

Both options install the `git-clone` and `flake8` tasks into your cluster under the currently active Kubernetes namespace.

After installing the required catalog tasks, apply your local tasks file:

```bash
kubectl apply -f tasks.yaml

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

::page{title="Step 1: Use the buildah ClusterTask"}

Your pipeline currently has a placeholder for a `build` step that uses the `e&#8203;cho` task. Now it is time to replace it with a real image builder.

To build container images, this lab uses the `buildah` task, which is already available in the OpenShift environment as a **ClusterTask**. Since ClusterTasks are installed cluster-wide by an administrator, they can be referenced directly in pipelines without any additional installation.

In this lab, you will reference the existing `buildah` ClusterTask when updating your pipeline configuration.

::page{title="Step 2: Add a Workspace to the Pipeline Task"}

Now you will update the `pipeline.yaml` file to use the new `buildah` task.

Open `pipeline.yaml` in the editor. To open the editor, click the button below.

&nbsp;

::openFile{path="/home/project/wtecc-CICD_PracticeCode/labs/05_build_an_image/pipeline.yaml"}

In reading the documentation for the **buildah** task, you will notice that it requires a workspace named `source`.

### Your Task

Add the workspace to the `build` task after the name, but before the `taskRef`. The workspace that you have been using is named `pipeline-workspace` and the name the task requires is `source`.

```yaml
    - name: build
      ... add code here...
      taskRef:

```

### Hint

<details>
<summary>Click here for a hint.</summary>
Use the `workspaces` keyword with a `name` of "source" and a `workspace` with the name of "pipeline-workspace".
</details>

### Solution

<details>
<summary>Click here for the answer.</summary>
<pre><code class="language-yaml">    - name: build
      workspaces:
        - name: source
          workspace: pipeline-workspace
      taskRef:
</code></pre>
</details>

::page{title="Step 3: Reference the buildah Task"}

Now, you need to reference the new buildah task that you want to use. In the previous steps, you simply changed the name of the reference to the task. But since the `buildah` task is a **ClusterTask**, you need to add the statement `kind: ClusterTask` under the name so that Tekton knows to look for a **ClusterTask** and not a regular **Task**.

### Your Task

Change the `taskRef` from `e&#8203;cho` to reference the `buildah` task and add a line below it with `kind: ClusterTask` to indicate that this is a ClusterTask:

### Solution

<details>
<summary>Click here for the answer.</summary>
<pre><code class="language-yaml">      taskRef:
        name: buildah
		kind: ClusterTask
</code></pre>
</details>

::page{title="Step 4: Update the Task Parameters"}

The documentation for the buildah task details several parameters but only one of them is required. You need to use the `IMAGE` parameter to hold the name of the image you want to build.

Since you might want to reuse this pipeline to build different images, you will make it a variable parameter that can be passed in when the pipeline runs. To do this, you need to change it here and add a parameter to the Pipeline itself.

### Your Task

Change the `message` parameter to `IMAGE` and specify the value of `$(params.build-image)`:

### Solution 1

<details>
<summary>Click here for the answer.</summary>
<pre><code class="language-yaml">      params:
      - name: IMAGE
        value: "$(params.build-image)"
</code></pre>
</details>

Now that you are passing in the `IMAGE` parameter to this task, you need to go back to the top of the `pipeline.yaml` file and add the parameter there so that it can be passed into the pipeline when it is run.

Add a parameter named `build-image` to the existing list of parameters at the top of the pipeline under `spec.params`.

### Solution 2

<details>
<summary>Click here for the answer.</summary>
<pre><code class="language-yaml">spec:
  params:
    - name: build-image
</code></pre>
</details>

::page{title="Step 5: Check Your Work"}

## Code Check

If you changed everything correctly, the full `build` task in the pipeline should look like this:

```yaml
    - name: build
      workspaces:
        - name: source
          workspace: pipeline-workspace
      taskRef:
        name: buildah
		kind: ClusterTask
      params:
      - name: IMAGE
        value: "$(params.build-image)"
      runAfter:
        - tests

```

Save your changes before you continue.

## Terminal Folder Check

Before you proceed with running commands in the terminal, make sure that you are in the `/home/project/wtecc-CICD_PracticeCode/labs/05_build_an_image` folder.

Go to the terminal and use the `p&#8203;wd` command just to be sure.

```bash
pwd

```

You should see: `/home/project/wtecc-CICD_PracticeCode/labs/05_build_an_image`. If you do not, you should `c&#8203;d` into that folder now:

```bash
cd /home/project/wtecc-CICD_PracticeCode/labs/05_build_an_image

```

You are now ready to execute the terminal commands in the next step.

::page{title="Step 6: Apply Changes and Run the Pipeline"}

## Apply the Pipeline

Apply the same changes you just made to `pipeline.yaml` to your cluster:

```bash
kubectl apply -f pipeline.yaml

```

## Apply the PVC

Next, make sure that the persistent volume claim for the workspace exists by applying it using `kubectl`:

```bash
kubectl apply -f pvc.yaml

```

## Start the Pipeline

When you start the pipeline, you need to pass in the `build-image` parameter, which is the name of the image to build.

This will be different for every learner that uses this lab. Here is the format:

_image-registry.openshift-image-registry.svc:5000/$SN\_ICR\_NAMESPACE/tekton-lab:latest_

Notice the variable `$SN_ICR_NAMESPACE` in the image name. This is automatically set to point to your container namespace.

Now, start the pipeline to see your new build task run. Use the Tekton CLI `pipeline start` command to run the pipeline, passing in the parameters `repo-url`, `branch`, and `build-image` using the `-p` option. Specify the workspace `pipeline-workspace` and volume claim `pipelinerun-pvc` using the `-w` option:

```bash
tkn pipeline start cd-pipeline \
    -p repo-url="https://github.com/ibm-developer-skills-network/wtecc-CICD_PracticeCode.git" \
	-p branch=main \
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

::page{title="Conclusion"}

Congratulations! You have just added the ability to build a Docker image and push it to the image registry in OpenShift.

In this lab, you learned how to use the `buildah` ClusterTask from the Tekton catalog. You learned how to modify your pipeline to reference the task as a ClusterTask and configure its parameters. You also learned how to pass additional parameters to a pipeline, how to run it to build an image, and how to push the image to an image registry in OpenShift.

## Next Steps

Try to set up a pipeline to build an image with Tekton from one of your own code repositories.

If you are interested in continuing to learn about Kubernetes and containers, you should get your own [free Kubernetes cluster](https://www.ibm.com/cloud/container-service/?utm_source=skills_network&utm_content=in_lab_content_link&utm_id=Lab-IBM-CD0215EN-SkillsNetwork) and your own free [IBM Container Registry](https://www.ibm.com/cloud/container-registry?utm_source=skills_network&utm_content=in_lab_content_link&utm_id=Lab-IBM-CD0215EN-SkillsNetwork).

Take the next step from building containers to optimizing them — try IBM Turbonomic free at [ibm.biz/snp-turbo.](https://ibm.biz/snp-turbo)

## Author(s)

[John J. Rofrano](https://www.coursera.org/instructor/johnrofrano)

### Other Contributor(s)

### © IBM Corporation . All rights reserved.

&nbsp;

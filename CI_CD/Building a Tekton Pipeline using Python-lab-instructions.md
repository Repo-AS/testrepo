::page{title="Building a Tekton Pipeline using Python"}

<img src="https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBM-CD0215EN-SkillsNetwork/images/IDSN-logo.png" width="200" />

**Estimated time needed:** 40 minutes

Welcome to the hands-on lab for **Building a Tekton Pipeline**. In this lab, you will create a simple Tekton pipeline with one task in Step 1 and then add a parameter to it in Step 4. You will learn best practices for structuring a Tekton pipeline project and how to author Tekton pipelines and tasks so that they are easy to use and parameterize. You will see that Tekton allows you to reuse your pipeline-as-code artifacts, and you will look at practical approaches to publishing your pipeline and task definitions to a Git repository.

## Learning Objectives

After completing this lab, you will be able to:

-   Create a base pipeline and task to echo a message.
    
-   Apply parameters to the task and pipeline.
    
-   Apply additional parameters to a pipeline to clone a Git repository.
    
-   Tekton pipeline definitions can be complex — and IBM Bob helps developers write and debug Kubernetes-native CI/CD configurations with AI assistance. Bob understands Tekton's task and pipeline YAML structure, helping you get your pipeline definitions right and troubleshoot issues quickly. Get started with a free trial at [ibm.biz/snp-bob.](https://ibm.biz/snp-bob)
    

## Prerequisites

You will need the following to complete the exercises in this lab:

-   A basic understanding of YAML
    
-   A GitHub account
    
-   An intermediate-level knowledge of CLIs
    

* * *

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
cd wtecc-CICD_PracticeCode/labs/01_base_pipeline/

```

## Navigate to the Labs Folder

Navigate to the `labs/01_base_pipeline` folder in left explorer panel. All of your work will be completed with the files in this folder.

![File Explorer](https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBM-CD0215EN-SkillsNetwork/images/01_file_explorer.png "Labs folder in explorer panel")

You are now ready to start the lab.

### Optional

If working in the terminal becomes difficult because the command prompt is very long, you can shorten the prompt using the following command:

```bash
export PS1="[\[\033[01;32m\]\u\[\033[00m\]: \[\033[01;34m\]\W\[\033[00m\]]\$ "

```

* * *

::page{title="Step 1: Create an echo Task"}

In true computer programming tradition, the first task you create will echo "Hello World!" to the console.

There is starter code in the `labs/01_base_pipeline` folder for a task and a pipeline. Navigate to this folder in left explorer panel, and open the `tasks.yaml` file to edit it:

&nbsp;

::openFile{path="/home/project/wtecc-CICD_PracticeCode/labs/01_base_pipeline/tasks.yaml"}

It should look like this:

```yaml
apiVersion: tekton.dev/v1beta1
kind: Task
metadata:
  name: <place-name-here>
spec:
  steps:

```

You will now create a **hello-world** task.

### Your Task

1.  The first thing you want to do is give the task a good name. Change `<place-name-here>` to `hello-world`.
    
2.  The next thing is to add a step that run a single command to include `name`, `image`, `command`, and `args`. Make the name `e&#8203;cho`, use the image `alpine:3`, have the command be `[/bin/echo]` and the args be `["Hello World"]`.
    

### Hint

<details>
<summary>Click here for a hint.</summary>
Add a step under the `steps:` tag. Since there can be multiple steps, each one starts with a dash `-` to identify it as an item in a `yaml` list.

<pre><code class="language-yaml">spec:
  steps:
    - name: {name here}
      image: {image here}
      command: {command here}
      args: {args here}
</code></pre>
</details>

Double-check that your work matches the solution below.

### Solution

<details>
<summary>Click here for the answer.</summary>
<pre><code class="language-yaml">apiVersion: tekton.dev/v1beta1
kind: Task
metadata:
  name: hello-world
spec:
  steps:
    - name: echo
      image: alpine:3
      command: [/bin/echo]
      args: ["Hello World!"]
</code></pre>
</details>

Apply it to the cluster:

```bash
kubectl apply -f tasks.yaml

```

* * *

::page{title="Step 2: Create a hello-pipeline Pipeline"}

Next, you will create a very simple pipeline that only calls the `hello-world` task that you just created. Navigate to this folder in left explorer panel, and open the `pipeline.yaml` file to edit it:

&nbsp;

::openFile{path="/home/project/wtecc-CICD_PracticeCode/labs/01_base_pipeline/pipeline.yaml"}

It should look like this:

```yaml
apiVersion: tekton.dev/v1beta1
kind: Pipeline
metadata:
  name: <place-name-here>
spec:
  tasks:

```

You will now create a **hello-pipeline** pipeline.

### Your Task

1.  The first thing you want to do is give the pipeline a good name. Change `<place-name-here>` to `hello-pipeline`.
    
2.  The next thing is to add a reference to the hello-world task you just created which needs a `name:` for the pipeline task, and a `taskRef:`, with a `name:` tag under it set to the name of the task you are referencing. Set the name of the pipeline task to `hello` and the name of the task you are referencing as `hello-world`.
    

### Hint

<details>
<summary>Click here for a hint.</summary>
Add a task under the `tasks:` tag. Since there can be multiple tasks, each one starts with a dash `-` to identify it as an item in a `yaml` list.

<pre><code class="language-yaml">spec:
  tasks:
    - name: {name here}
      taskRef:
        name: {task name here}
</code></pre>
</details>

Double-check that your work matches the solution below.

### Solution

<details>
<summary>Click here for the answer.</summary>
<pre><code class="language-yaml">apiVersion: tekton.dev/v1beta1
kind: Pipeline
metadata:
  name: hello-pipeline
spec:
  tasks:
    - name: hello
      taskRef:
        name: hello-world
</code></pre>
</details>

Apply it to the cluster:

```bash
kubectl apply -f pipeline.yaml

```

You are now ready to run your pipeline and see if it works.

* * *

::page{title="Step 3: Run the hello-pipeline"}

Run the pipeline using the Tekton CLI:

```bash
tkn pipeline start --showlog hello-pipeline

```

You should see the output:

```
PipelineRun started: hello-pipeline-run-9vkbb
Waiting for logs to be available...
[hello : echo] Hello World!

```

Congratulations! You just ran your first pipeline from a pipeline and task that you created.

* * *

::page{title="Step 4: Add a parameter to the task"}

Hopefully the hello-world task has given you a sense for how pipelines call tasks. Now it is time to make that task a little more useful by making it print any message that you want, not just "Hello World".

To do this, you will add a parameter called `message` to the task and use that parameter as the message that it echoes. You will also rename the task to `e&#8203;cho`.

Edit the `tasks.yaml` file to add the parameter to both the input and the echo command:

&nbsp;

::openFile{path="/home/project/wtecc-CICD_PracticeCode/labs/01_base_pipeline/tasks.yaml"}

### Your Task

1.  Change the name of the task from `hello-world` to `e&#8203;cho` to more acurately reflect its new functionality, by changing the `name:` in the `metadata:` section.
    
2.  Add a `params:` section to the task with a parameter that has a `name:` of "message", a `type:` of "string", and a `description` of "The message to echo".
    
3.  Change the name of the step from `e&#8203;cho` to `echo-message` to better describe its new functionality.
    
4.  Modify the `args:` tag to use the message parameter you just created.
    

### Hint

<details>
<summary>Click here for a hint.</summary>
Add a `params:` section under the `spec:` tag. Since there can be multiple parameters, each one starts with a dash `-` to identify it as an item in a `yaml` list.

<p>The reference to the message parameter should be <code>$(params.message)</code>.</p><pre><code class="language-yaml">metadata:
  name: {change the task name}
spec:
  params:
    - name: {name here}
      description: {description here}
      type: {type here}
  steps:
    - name: echo-message
      image: alpine:3
      command: [/bin/echo]
      args: {place parameter reference here}
</code></pre>
</details>

Double-check that your work matches the solution below.

### Solution

<details>
<summary>Click here for the answer.</summary>
<pre><code class="language-yaml">apiVersion: tekton.dev/v1beta1
kind: Task
metadata:
  name: echo
spec:
  params:
    - name: message
      description: The message to echo
      type: string
  steps:
    - name: echo-message
      image: alpine:3
      command: [/bin/echo]
      args: ["$(params.message)"]
</code></pre>
</details>

Apply the new task definition to the cluster:

```bash
kubectl apply -f tasks.yaml

```

* * *

::page{title="Step 5: Update the hello-pipeline"}

You now need to update the pipeline to pass the message that you want to send to the `e&#8203;cho` task so that it can echo the message to the console.

Edit the `pipeline.yaml` file to add the parameter:

&nbsp;

::openFile{path="/home/project/wtecc-CICD_PracticeCode/labs/01_base_pipeline/pipeline.yaml"}

### Your Task

1.  Add a `params:` section to the pipeline under `spec:`, with a parameter that has a `name:` of "message".
    
2.  Change the `name:` of the `taskRef:` from `hello-world` to the new `e&#8203;cho` task.
    
3.  Add a `params:` section to the task, with a parameter that has a `name:` of "message" and a `value:` that is a reference to the pipeline parameter for `params.message`.
    

### Hint

<details>
<summary>Click here for a hint.</summary>
Specify the value of message params in tasks as "$(params.message)".

<pre><code class="language-yaml">spec:
  params:
    - name: {parameter name here}
  tasks:
    - name: hello
      taskRef:
        name: {change parameter value here}
      params:
        - name: {task parameter name here}
          value: "$(params.message)"
</code></pre>
</details>

Double-check that your work matches the solution below.

### Solution

<details>
<summary>Click here for the answer.</summary>
<pre><code class="language-yaml">apiVersion: tekton.dev/v1beta1
kind: Pipeline
metadata:
  name: hello-pipeline
spec:
  params:
    - name: message
  tasks:
    - name: hello
      taskRef:
        name: echo
      params:
        - name: message
          value: "$(params.message)"
</code></pre>
</details>

Apply it to the cluster:

```bash
kubectl apply -f pipeline.yaml

```

* * *

::page{title="Step 6: Run the message-pipeline"}

Run the pipeline using the Tekton CLI:

```bash
tkn pipeline start hello-pipeline \
    --showlog  \
    -p message="Hello Tekton!"

```

You should see the output:

```
PipelineRun started: hello-pipeline-run-9qf42
Waiting for logs to be available...
[hello : echo-message] Hello Tekton!

```

Congratulations! You just created and ran a pipeline that requires a parameter.

* * *

::page{title="Step 7: Create a checkout Task"}

In this step, you will combine your knowledge of running a command in a container with your knowledge of passing parameters, to create a task that checks out your code from GitHub as the first step in a CD pipeline.

## Create checkout task

You can have multiple definitions in a single yaml file by separating them with three dashes `---` on a single line. In this step, you will add a new task to `tasks.yaml` that uses the `bitnami/git:latest` image to run the `g&#8203;it` command passing in the branch name and URL of the repo you want to clone.

Open the `tasks.yaml` file to create a new task:

&nbsp;

::openFile{path="/home/project/wtecc-CICD_PracticeCode/labs/01_base_pipeline/tasks.yaml"}

Add three dashes on a separate line:

```yaml
---

```

You are now ready to add your new task.

### Your Task

Your new task will create a Tekton task that accepts a repository URL and a branch name and calls `g&#8203;it clone` to clone your source code.

1.  Create a new task and name it `checkout`.
    
2.  Add a parameter named `repo-url` with a `type:` of string and a `description:` of "The URL of the git repo to clone".
    
3.  Add a second parameter named `branch` with a `type:` of string and a `description:` of "The branch to clone".
    
4.  Add a step with the `name:` "checkout" that uses the `bitnami/git:latest` image to run the `g&#8203;it` command by specifying `clone` and `--branch` parameters and passing both the params created in spec as the arguments.
    

### Hint

<details>
<summary>Click here for a hint.</summary>
Pass arguments to the checkout task as ["clone", "--branch", "<span data-type="math-inline" data-content="(params.branch)&quot;, &quot;"></span>(params.repo-url)"].

<pre><code class="language-yaml">apiVersion: tekton.dev/v1beta1
kind: Task
metadata:
  name: {name of task here}
spec:
  params:
    - name: {1st parameter name here}
      description: {1st parameter name here}
      type: string
    - name: {2nd parameter name here}
      description: {2nd parameter name here}
      type: string
  steps:
    - name: {step name here}
      image: {image name here}
      command: [{command name here}]
      args: [{arguments here}]
</code></pre>
</details>

Double-check that your work matches the solution below.

### Solution

<details>
<summary>Click here for the answer.</summary>
<pre><code class="language-yaml">---
apiVersion: tekton.dev/v1beta1
kind: Task
metadata:
  name: checkout
spec:
  params:
    - name: repo-url
      description: The URL of the git repo to clone
      type: string
    - name: branch
      description: The branch to clone
      type: string
  steps:
    - name: checkout
      image: bitnami/git:latest
      command: [git]
      args: ["clone", "--branch", "$(params.branch)", "$(params.repo-url)"]
</code></pre>
</details>

Apply it to the cluster:

```bash
kubectl apply -f tasks.yaml

```

Your output should look like this:

```txt
task.tekton.dev/echo configured
task.tekton.dev/checkout created

```

The `e&#8203;cho` task was unchanged and the `checkout` task has been created.

* * *

::page{title="Step 8: Create the cd-pipeline Pipeline"}

Finally, you will create a pipeline called `cd-pipeline` to be the starting point of your Continuous Delivery pipeline.

Open the `pipeline.yaml` file to create a new pipeline called `cd-pipeline`:

&nbsp;

::openFile{path="/home/project/wtecc-CICD_PracticeCode/labs/01_base_pipeline/pipeline.yaml"}

You can use `---` on a separate line to separate your new pipeline, or you can modify the existing pipeline to look like the new one.

### Your Task

1.  Create a new pipeline and name it `cd-pipeline`.
    
2.  Add two parameters named `repo-url` and `branch`.
    
3.  Set the `default:` for **branch** to "master".
    
4.  Add a task with the `name:` "clone" that has a `taskRef:` to the `checkout` task that you just created.
    
5.  Add the two parameters `repo-url` and `branch` to the task, mapping them back to the pipeline parameters of the same name.
    

### Hint

<details>
<summary>Click here for a hint.</summary>
Add params of name `repo-url` and `branch` with values as "<span data-type="math-inline" data-content="(params.repo-url)&quot; and &quot;"></span>(params.branch)" to the `clone` task.

<pre><code class="language-yaml">spec:
  params:
    - name: {1st parameter name here}
    - name: {2nd parameter name here}
      default: {default value here}
  tasks:
    - name: {pipeline task name here}
      taskRef:
        name: {Task name here}
      params:
      - name: {1st parameter name here}
        value: "$(params.repo-url)"
      - name: {2nd parameter name here}
        value: "$(params.branch)"
</code></pre>
</details>

Double-check that your work matches the solution below.

### Solution

<details>
<summary>Click here for the answer.</summary>
<pre><code class="language-yaml">---
apiVersion: tekton.dev/v1beta1
kind: Pipeline
metadata:
  name: cd-pipeline
spec:
  params:
    - name: repo-url
    - name: branch
      default: "master"
  tasks:
    - name: clone
      taskRef:
        name: checkout
      params:
      - name: repo-url
        value: "$(params.repo-url)"
      - name: branch
        value: "$(params.branch)"
</code></pre>
</details>

Apply it to the cluster:

```bash
kubectl apply -f pipeline.yaml

```

* * *

::page{title="Step 9: Run the cd-pipeline"}

Run the pipeline using the Tekton CLI:

```bash
tkn pipeline start cd-pipeline \
    --showlog \
    -p repo-url="https://github.com/ibm-developer-skills-network/wtecc-CICD_PracticeCode.git" \
    -p branch="main"

```

The output should look like this:

```
PipelineRun started: cd-pipeline-run-rf6zp
Waiting for logs to be available...
[clone : checkout] Cloning into 'wtecc-CICD_PracticeCode'...

```

* * *

::page{title="Step 10: Fill Out cd-pipeline with Placeholders"}

In this final step, you will fill out the rest of the pipeline with calls to the `e&#8203;cho` task to simply display a message for now. You will replace these "placeholder" tasks with real ones in future labs.

Update the pipeline.yaml file to include four placeholder tasks.

&nbsp;

::openFile{path="/home/project/wtecc-CICD_PracticeCode/labs/01_base_pipeline/pipeline.yaml"}

Now you will add four tasks to the pipeline to lint, unit test, build, and deploy. All of these pipeline tasks will reference the `e&#8203;cho` task for now.

### Your Task

Create a pipeline task for each of these:

| Task Name | Build After | Message |
| --- | --- | --- |
| lint | clone | Calling Flake8 linter... |
| tests | lint | Running unit tests with PyUnit... |
| build | tests | Building image for $(params.repo-url) ... |
| deploy | build | Deploying $(params.branch) branch of $(params.repo-url) ... |

### Hint

<details>
<summary>Click here for a hint.</summary>
Add params of name `repo-url` and `branch` with values as "<span data-type="math-inline" data-content="(params.repo-url)&quot; and &quot;"></span>(params.branch)" to the `clone` task.

<pre><code class="language-yaml">spec:
  tasks:
    - name: {pipeline task name here}
      taskRef:
        name: echo
      params:
      - name: message
        value: {message to display here}
      runAfter:
        - {name of previous task}

	...
</code></pre>
</details>

You now have a base pipeline to build the rest of your tasks into.

Double-check that your work matches the solution below.

### Solution

<details>
<summary>Click here for the answer.</summary>
<pre><code class="language-yaml">---
apiVersion: tekton.dev/v1beta1
kind: Pipeline
metadata:
  name: cd-pipeline
spec:
  params:
    - name: repo-url
    - name: branch
      default: "master"
  tasks:
    - name: clone
      taskRef:
        name: checkout
      params:
      - name: repo-url
        value: "$(params.repo-url)"
      - name: branch
        value: "$(params.branch)"

    - name: lint
      taskRef:
        name: echo
      params:
      - name: message
        value: "Calling Flake8 linter..."
      runAfter:
        - clone

    - name: tests
      taskRef:
        name: echo
      params:
      - name: message
        value: "Running unit tests with PyUnit..."
      runAfter:
        - lint

    - name: build
      taskRef:
        name: echo
      params:
      - name: message
        value: "Building image for $(params.repo-url) ..."
      runAfter:
        - tests

    - name: deploy
      taskRef:
        name: echo
      params:
      - name: message
        value: "Deploying $(params.branch) branch of $(params.repo-url) ..."
      runAfter:
        - build
</code></pre>
</details>

Apply it to the cluster:

```bash
kubectl apply -f pipeline.yaml

```

* * *

::page{title="Step 11: Run the cd-pipeline"}

Run the pipeline using the Tekton CLI:

```bash
tkn pipeline start cd-pipeline \
    --showlog \
    -p repo-url="https://github.com/ibm-developer-skills-network/wtecc-CICD_PracticeCode.git" \
    -p branch="main"

```

The output will look like this:

```
PipelineRun started: cd-pipeline-run-wvfzx
Waiting for logs to be available...
[clone : checkout] Cloning into 'wtecc-CICD_PracticeCode'...

[lint : echo-message] Calling Flake8 linter...

[tests : echo-message] Running unit tests with PyUnit...

[build : echo-message] Building image for https://github.com/ibm-developer-skills-network/wtecc-CICD_PracticeCode.git ...

[deploy : echo-message] Deploying main branch of https://github.com/ibm-developer-skills-network/wtecc-CICD_PracticeCode.git ...

```

::page{title="Conclusion"}

Congratulations! You are now able to create a Tekton pipeline and pass parameters to a pipeline.

In this lab, you learned how to create a base pipeline, specify and pass parameteres to a task and pipeline. You learned how to modify your pipeline to reference the task and configure its parameters. You also learned how to pass additional parameters to a pipeline and how to run it to echo and clone a Git repository.

## Next Steps

You will learn and use GitHub Triggers in the next lab.

Write Tekton pipelines with AI-powered assistance — try Bob free at [ibm.biz/snp-bob.](https://ibm.biz/snp-bob)

## Author(s)

Tapas Mandal [John J. Rofrano](https://www.coursera.org/instructor/johnrofrano)

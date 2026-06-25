::page{title="Evaluating Vulnerability Analysis"}

**Estimated time needed:** 20 minutes

## Introduction

Welcome to the hands-on lab for **Evaluating Vulnerability Analysis**.

When you are tasked with developing a secure application, building security into the software development lifecycle is important. However, that does not guarantee that your app will be free from vulnerabilities when it is time to deploy it. Performing a vulnerability analysis can help you identify vulnerabilities lurking inside your app before it goes live.

A vulnerability analysis involves a systematic and thorough review of possible known weaknesses or vulnerabilities in a system or application. Revealing vulnerabilities is the first step in remedying the issue and developing a secure system.

## Learning Objectives

After completing this lab, you will be able to:

- Perform a vulnerability scan on a sample web application using the pip audit tool
- Evaluate the results of the vulnerability scan
- Explain why performing vulnerability analyses are essential to developing secure software applications

::page{title="Set up the Lab Environment"}

You have a little preparation to do before you can start the lab. In the following steps, you will download and install a vulnerability scanner along with a sample web application to test against.

For this lab, you will use:

- pip-audit, an open-source Python dependency vulnerability scanner
- Hit Counter, a sample Python Flask web application

**What is pip-audit?**

pip-audit is an open-source vulnerability scanner developed by the Python Packaging Authority (PyPA). It scans Python dependencies and checks them against known vulnerability databases such as the Python Advisory Database. It is commonly used to identify vulnerable packages in Python applications.

**What is Hit Counter?**

Hit Counter is a Python Flask application that has not been updated recently. It uses older dependency versions, making it a good candidate for demonstrating vulnerability analysis. For example, it depends on an outdated version of Flask, which may contain known security vulnerabilities.


::page{title="Step 1:  Install the pip-audit Tool"}

You will install pip-audit using Python\'s package manager inside a virtual environment.

### Your Task

Open a new terminal from the top menu:
**Terminal → New Terminal, and navigate to the project directory:**

```bash
cd /home/project
```

![Image of opening new terminal](https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBM-CD0267EN-SkillsNetwork/images/new_terminal_box_red.png "Image of opening new terminal")

Install Python virtual environment support:
```bash
sudo apt-get update && sudo apt-get install -y python3-venv
```

Create and activate a Python virtual environment:

```bash
python3 -m venv venv
source venv/bin/activate
```

Verify that the virtual environment is active:
```bash
which python
```

![Image of venv output](https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBM-CD0267EN-SkillsNetwork/images/vul_venv_output.png "Image of venv output")
> You should see `(venv)` before the prompt and `which python` should return `/home/project/venv/bin/python`. If you see both of these, everything is working properly.

You should see output similar to:

```/home/project/venv/bin/python```


Install pip-audit in the virtual environment:

```bash
pip install pip-audit
```

Verify that pip-audit is installed correctly:

```bash
pip-audit --help
```
## Results

You should see the following output:

![pip ss 1.png](https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/mM_whbMozf8z_1kd7Z62WA/pip%20ss%201.png)

::page{title="Step 2: Install the code to scan"}

Now that you have your vulnerability scanning tool installed, you will also need an application to scan for vulnerabilities. You will use a Python Flask application that is called **Hit Counter**. It has some outdated dependencies, which will provide a good example for vulnerability analysis.


### Your Task

Clone the Hit Counter application repository:

```bash
git clone https://github.com/ibm-developer-skills-network/ycuer-flask-hitcounter.git
```

Change into the project directory:

```bash
cd ycuer-flask-hitcounter
```

Install the application\'s Python dependencies from the requirements.txt file:

```bash
pip install -r requirements.txt
```

You are now ready to scan the Hit Counter application for vulnerabilities.

::page{title="Step 3: Running a Vulnerability Scan"}

With the application dependencies installed, you can now run a vulnerability scan using ```pip-audit```.

### Your Task

From the ```ycuer-flask-hitcounter directory```, run:

```bash
pip-audit
```
### Results

The output will list the Python packages used by the application and identify any known vulnerabilities. The results may vary depending on when you run the lab, as vulnerability databases are updated regularly.

**The scan output will include:**
- The name of the vulnerable package
- The installed version
- The vulnerability ID (CVE or advisory ID)
- A brief description of the issue

::page{title="Step 4: Interpreting the Results"}

The scan analyzes the application\'s dependencies and identifies packages with known security vulnerabilities.

You will typically see:

- A summary of vulnerable dependencies

- Details about each vulnerability, including severity and advisory information

- Suggested remediation steps, such as upgrading to a secure version

![pip output ss2.png](https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/E_DMG1_IpybTUrsQ5FGkZw/pip%20output%20ss2.png)

For example, the scan may show that Flask 1.1.4 contains known vulnerabilities. This indicates that the dependency should be upgraded to a newer, patched version.

To remediate vulnerabilities, you would usually update the affected package versions in the requirements.txt file and rerun the scan to confirm the issues are resolved.

::page{title="Conclusion"}

Congratulations! You have successfully completed a vulnerability scan on a web application using pip-audit. Vulnerability scanning is a critical skill for developing and maintaining secure software.

In this lab, you learned how to:

- Perform a vulnerability analysis on a Python application

- Review and interpret vulnerability scan results

- Understand how dependency vulnerabilities impact application security

Vulnerability analysis is an iterative process that involves identifying vulnerabilities, assessing risk, remediating issues, and rescanning to verify fixes.

## Next Steps

Apply this knowledge to your own Python projects by running pip-audit regularly. Most vulnerabilities can be resolved by updating dependency versions in your requirements.txt file. Always validate fixes by rerunning vulnerability scans.

## Author

Alima Akhter

### Other Contributor(s)

Sam Propochuk

Michelle R. Sanchez, Instructional Designer at Skill-up Technologies with over 25 years of enterprise-level technical training and support experience.

<!--## Changelog
| Date | Version | Changed by | Change Description |
|------|--------|--------|---------|
| 2022-08-21 | 0.1 | David Pasternak | Initial version created |
| 2022-08-26 | 0.2 | John Rofrano | Split into more steps for clarity |
| 2022-09-08 | 0.3 | Michelle Sanchez | Corrective edits |
| 2022-09-28 | 0.4 | John Rofrano | Rewrote using Jake and Python code |
| 2022-09-29 | 0.5 | Amy Norton | ID review |
| 2022-09-30 | 0.5 | Steve Hord | QA pass edits |-->
<h3 align="center"> &#169; IBM Corporation. All rights reserved. <h3/>

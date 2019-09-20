---
layout: post
title: Jenkins Pipeline Script to get build/environment variables from the child job.
---

Sometimes, It is useful to have your Jenkins job return the required parameters to continue further in the work flow. 

Let us assume we have JobA calling JobB, JobA takes few paramters used in JobB to resume work.

We can achive the same in Jenkins Pipeline as explained below. 

```
stage('JobA') {
    state = "Failed in JobA"
    def JobB_Result = build job: 'JobB', parameters: [string(name: 'abc', value: var1), string(name: 'xyz', value: var2)]
    def JobB_env = JobB_Result.getBuildVariables()
    # You can use the JobB_env further in the code. JobB_env is the keypair with all build/environment variables from JobB.
    }
``` 

In case if your looking at a particular environment variable. Use the following 

```
def JobB_varx = JobB_Result.getBuildVariables().get('varx')
```

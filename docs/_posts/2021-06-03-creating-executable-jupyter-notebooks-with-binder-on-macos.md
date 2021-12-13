---
layout:	post
title:	"Creating Executable Jupyter Notebooks with Binder on macOS"
description: A discussion of why Jupyter Notebooks are useful and how to fix errors with Binder builds online. 
date:	2021-06-03
featured_image: '/img/stamp.jpeg'
tags: jupyter-notebook binder conda yml python 
author: Kostya Farber
---

## Reproducibility
One of the foundational pillars of the scientific method is **reproducibility**. One of the advantages of reproducibility is transparency and the ability for other experimenters to attempt to verify your results or play around with the experiment that you created. The analogous method in which we create reproducibility in a computing context is by creating virtual environments. This tutorial will be using [**Conda**](https://docs.conda.io/en/latest/), a package, dependency and environment management system that is popular in the data science community.
## Jupyter Notebooks
[Jupyter Notebooks](https://jupyter.org/) are a popular way for scientists to explore their data. It provides a way to show your results alongside your code. Users may download your notebook and play around with your code and try replicate your results. 

The key for this to work however, is making sure the user is able to run the notebook on their machine (Windows, Mac or Linux). The first step in the process is making sure you create a virtual environment and download all the packages and dependencies for your project there. This is mainly to ensure that the user is able to determine exactly what packages and versions they need to run your notebook. They can install those packages into their environment easily with this information. 

However, we can take this one step further. Instead of making the user replicate the environment on their machine, we may host our environment online and create a fully executable notebook. This makes it even easier and more accessible for others to experiment with your code and reproduce your computing environment and results.

## The Binder Project
[Binder](https://jupyter.org/binder) is exactly that. The Binder project offers an easy place to share computing environments to everyone. It allows users to specify custom environments and share them with a single link. Use-cases involve workshops, scientific workflows and streamline sharing among teams. 

![](/img/1*FEiQ3UjmMmpYY3t9m5Pf1g.gif)

The Binder Project builds tools that reward best-practices in reproducible data science by utilizing community-developed standards for reproducibility. When repositories follow these best-practices and are hosted in an online repository, then Binder automatically builds a linkable environment anybody can access.Binder offers a way to extend that reproducibility and make it even easier to recreate computing environments with a single link. Binder conveniently is able to use repositories with Jupyter Notebooks hosted on [GitHub](https://github.com/) to create shareable environments. **It is as easy as copying the link into a web browser. However your operating system might make it a tad harder.**


## Docker, Operating Systems and Dependencies

Binder uses a tool called repo2docker which fetches a repository (from GitHub, GitLab, Zenodo, Figshare, Dataverse installations, a Git repository or a local directory) and builds a container image in which the code can be executed. The image build process is based on the configuration files found in the repository. As mentioned earlier we can use conda to produce those configuration files.

![](/img/1*8K9TOg-66VYhfWcUEAHs2g.gif)How to create a YAML configuration file from conda.However creating the environment.yml as is, will likely cause issues depending on which operating system your machine is running on. The docker container is built on a Ubuntu (Linux operating system) when Binder runs repo2docker. When we create the environment.yml the export actually lists dependencies that are *too**** ***specific. For example an entry might look like matplotlib==3.0.2=py36h54f8f79\_. The py=36xxxxxx suffix is actually **OS-dependent.** During export, packages are included in the configuration file that are specific to the operating system. This will cause the build to fail and our environment will *not be able to run.*

## How Do We Fix the Issue?

The problem consists of packages that are too specific and OS-dependent. For the first problem conda has flags that we can add to the export command that will tone done the specificity of the packages in the current environment during export. We can run the export as usual and add the --no-builds flag at the end. This will remove the OS related suffixes.

For the second problem, on Mac OS specifically, there are a few packages that are known to cause problems. These include:

* `libcxxabi=4.0.1`
* `appnope=0.1.0`
* `libgfortran=3.0.1`
* `libcxx=4.0.1`

For example, `appnope=0.1.0` exists only on Mac OS so when Ubuntu tries to find this package; it won’t be able to and the build will fail. So we need to manually prune the configuration file for these packages. Unfortunately `--no-builds` doesn’t remove all these packages nor any conda command for that matter at the time of writing.

Manually finding these packages, whilst not too tedious, is better made to be automatically removed. I created a python script below that will remove these packages from a **YAML** configuration file.

A simple script to remove those pesky packages. A couple of things about this script:

* Make sure that the `script.py` file is in the directory that includes your `environment.yml` file.
* Your second command-line argument should be the name of your environment file (i.e `python script.py` environment.yml).
* This will overwrite the current existing `environment.yml`. If you need to recover the original you can just run the conda commands again.

```python
import sys
import yaml
import re

with open(sys.argv[1], mode='r') as file:
    environment = yaml.safe_load(file)

    pattern = '.*libgfortran.*|.*appnope.*|.*libcxx.*'

    for package in environment['dependencies']:
        if isinstance(package, str):
            if re.search(pattern, package):

                environment['dependencies'].remove(package)

                print("Match found, {} removed".format(package))

with open(sys.argv[1], mode='w') as yml:
    yaml.dump(environment, yml)
```

## Conclusion

Binder is a wonderful tool for reproducibility. Better yet, the process can be as easy as copying a link; provided that you create the correct configuration file. This was the problem I came across when trying to create my own hosted environment and these are the steps I took to make the tool work on Mac OS. I hope this will help anyone that is stuck wondering why their build is always failing! Thanks for reading.

  
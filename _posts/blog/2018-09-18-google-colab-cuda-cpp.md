---
layout: post
title: "Run CUDA C/C++ in Jupyter notebook in Google Colaboratory"
modified: 2018-09-19
categories: blog
excerpt: a way to test cuda capability without buying/installing NVIDIA graphic cards
tags: [Windows, CUDA]
image:
  feature: google/google-colab-cuda-cpp.png
date: 2018-09-18
comments: true
share: true
---

I learnt to run cuda C/C++ program in google Colab using the Jupyter notebook from [here](https://medium.com/@iphoenix179/running-cuda-c-c-in-jupyter-or-how-to-run-nvcc-in-google-colab-663d33f53772). I will show some details of the implementations at a later time.

<!--more-->

Use the following command to install CUDA nvcc package:

```
!apt update -qq;
!wget https://developer.nvidia.com/compute/cuda/8.0/Prod2/local_installers/cuda-repo-ubuntu1604-8-0-local-ga2_8.0.61-1_amd64-deb;
!dpkg -i cuda-repo-ubuntu1604-8-0-local-ga2_8.0.61-1_amd64-deb;
!apt-key add /var/cuda-repo-8-0-local-ga2/7fa2af80.pub;
!apt-get update -qq;
!apt-get install cuda gcc g++ -y -qq;
!ln -s /usr/bin/gcc /usr/local/cuda/bin/gcc;
!ln -s /usr/bin/g++ /usr/local/cuda/bin/g++;
!apt install cuda-8.0;
```

Now you can test your CUDA installation by running
`!/usr/local/cuda/bin/nvcc --version`

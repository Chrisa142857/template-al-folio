---
layout: post
title: a post with formatting and links
date: 2023-05-24 11:41:16
description: fMRI data preprocessing
tags: fMRI, SPM, CONN toolbox, OASIS, Natlab, sMRI, fMRI
categories: sample-posts
---

This blog is a hand-by-hand tutorial for researchers who in [ACMLab](https://acmlab.org/) to process MRI data. In the meantime, make an effort for the development of the computational neuroimaging field.

## 0. Install Software

 - Matlab. 
 - CONN toolbox (Download .zip: link. Source page: link). Unzip it.
 - SPM (Download .zip: link. Source page: link). Unzip it.
 - Start Matlab, click on the 'Set path' button, then click on 'Add folder', and select your CONN installation folder (e.g. /software/conn). After this, click again on 'Add folder' and now select the SPM installation folder (e.g. /software/spm12). Click on 'Save' and 'Close' to save these changes for future Matlab sessions
<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/post_conn_1.jpg" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Screenshot: Set path in Matlab.
</div>

 - Install python
    - Install a miniconda and python
    - Create an environment. Activate it.
    - Use `pip install nibabel numpy scipy`



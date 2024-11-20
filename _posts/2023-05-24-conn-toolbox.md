---
layout: post
title: Extracting RoI BOLD signal of fMRI dataset by using CONN toolbox
date: 2023-05-24 11:41:16
description: fMRI data preprocessing on OASIS3 as an example
tags: SPM, CONN toolbox, OASIS, Matlab, sMRI, fMRI
categories: neuroscience
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


## I. What data do you have: The input

Briefly, you need to collect all paths of the input T1w and fMRI volume, and remap the raw atlas label to 1~N with the corresponding label name in .txt file.

**One input of CONN toolbox is termed as `Subject`. It has one T1w and multiple fMRI.**

1. One T1-weighted (T1w) MRI volume (3D) for each subject.
For each subject, one T1w volume is enough.  You need to check the T1w you are collecting is in a valid format by reading the file header, like orientation and dimension. 
For example, OASIS3 T1w volume's orientation is indicated by header`['qform_code'] == 1`. And, the volume file name with 'echo' means it is 2D, which is not valid. 
Collect all paths in a file, where each line is one T1w of a subject.
2. At least one functional MRI volume (4D) at rest state or any task.
There might be multiple sessions and runs of fMRI scans for each subject. The pipeline requires the fMRI in one `subject` to have the same shape. So, you need to check the `header['dim']` of each fMRI to be the same. Otherwise, let it be a new `subject` with corresponding T1w volume. 
After data paths of T1w and fMRI are collected, you need to make sure how many fMRI sessions are matched to one T1w volume. And save those numbers.
3. Any atlas label volume (3D) in the MNI space, along with the look-up table.
Raw atlas files vary and depend on publishers. They might be in the surface format, if so, you need to convert it to volume first. Then, let the original label ID of the atlas volume remap to `[1, N]`, where N is the number of RoI. Along with the remapped atlas, the label name needs to be generated into a Txt file as the template in CONN toolbox.

## II. CONN step #1
1. Load the path of T1w, fMRI, and RoI: Copy path of subjects into CONN toolbox
2. Click preprocessing: Registration, segmentation
3. Click Done: Extract RoI

## III. CONN step #2
1. Choose all RoIs in the list: Set all RoIs for the following process
2. Click Done: Regression RoIs

3. Check output: We are done with CONN toolbox part. Go to the output directory and check this path. 

## IV. Get the output
BOLD timeseries are saved in `.mat` files.
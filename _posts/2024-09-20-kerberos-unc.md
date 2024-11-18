---
layout: post
title: Ubuntu 20.04 LTS configuring Kerberos client with PAM 
date: 2024-09-20 11:41:16
description: Take UNC Onyen server as an example
tags: Ubuntu 20.04, Kerberos, PAM, UNC
categories: sample-posts
---

It's hard to find an article showing how to configure a Kerberos client with PAM on Ubuntu 20.04 or higher. Here is the step-by-step tutorial 
## 0. Update apt

````bash
sudo apt-get update
sudo apt-get upgrade
````

## 1. Install packages and configure Kerberos source

````bash
sudo apt-get install krb5-user libpam-krb5
sudo vim /etc/krb5.conf
````

Here is an example configuration using UNC AD server:

````bash
[libdefaults]
# campus AD is now the authentication source
default_realm = AD.UNC.EDU
# for MIT Kerberos
kdc_timesync = 1
ccache_type = 4
forwardable = true
proxiable = true
# for Heimdal Kerberos
fcc-mit-ticketflags = true

[realms]
AD.UNC.EDU = {
    kdc = addc0.ad.unc.edu
    kdc = addc1.ad.unc.edu
    kdc = addc2.ad.unc.edu
    kdc = addc3.ad.unc.edu
    kdc = addc4.ad.unc.edu
}
````

## 2. Enable authentication via PAM
`sudo pam-auth-update`

Make sure you selected Kerberos authentication and do not select Unix, which has a higher priority.
<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/post_kerberos.jpg" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Screenshot: PAM configuration.
</div>

## 3. Verify the connection between Kerberos server
`kinit OnyenName`

## 4. Add users and verify the authentication
````bash
sudo adduser --home /path/to/home OnyenName
sudo login
````
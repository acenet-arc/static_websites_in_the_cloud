---
layout: page
title: "Instructor Notes"
permalink: /guide/
---

To create a VM for students to use for creating their first jekyll site use the `cloud_init_webserver.yml` file in the [cloud-init-files](../cloud-init-files/) folder when creating the VM to perform setup. Copy and paste the contents of that file into "Customization Script" under the "Configuration" tab in the popup while creating a VM in OpenStack.  The `cloud_init_webserver.yml` will need to have a few edits to setup a public key and username for the admin user, as well as the number of guest users. See notes in the file for details.

With a `p16-24gb` flavor VM, 30 guest users is a very comfortable number. As for storage, 1GB per user is also quite comfortable. With 30 guest users per VM, I went with 50GB root volume, should be more than enough space given that the site we are working with will only be a few MB.

This VM will also need to have HTTP port open in the security group rules to allow students to see their websites.

Once VM setup has completed have a look at the VM log on the OpenStack dashboard to find the login password for guest accounts. Search for "Guest accounts passphrase:".

Also, before users try to create their first jekyll site, some gems need to be installed for the theme I chose.

As a sudo user on the workshop VM (the admin user specified in the cloud-init file above) do the following to ensure regular users won't need to install those gems:

~~~
$ wget https://github.com/andrewbanchich/forty-jekyll-theme/archive/master.zip
$ unzip master.zip
$ cd forty-jekyll-theme-master
$ sudo bundle install
~~~
{: .bash}


then regular users should just have to do:
~~~
$ jekyll build -d /var/www/html/user01
~~~
{: .bash}

as in the workshop

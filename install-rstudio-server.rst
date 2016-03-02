===================================
Running RStudio Server in the cloud
===================================

Ref: https://www.rstudio.com/products/rstudio/download-server/

Start an m4.large ami-05384865:

----

Switch to zone US West (N California).

Launch instance.

Community AMIs.

Search for ami-05384865 (ubuntu-wily-15.10-amd64-server)

Select.

Choose m4.large.

Review and Launch.

Click Launch.

Create a new key pair.

name it 'amazon-key'.

Download key pair.

Launch instance.

View instances (lower right)

----

While it's going from yellow to green, find "Security Groups" in lower pane.
Click on "launch-wizard-N".

In lower pane of security groups page, click on Inbound, then Edit.

Add Rule.

Custom TCP, 8000-9000, Source Anywhere. Save.

Go back to Instances.

----

Find "Public DNS". This is your hostname.

Log in with ssh::

    ssh -i /path/to/amazon-key.pem ubuntu@ec2-54-153-33-165.us-west-1.compute.amazonaws.com

You will need to ``chmod og-rwx`` your amazon-key.pem first.

Once logged in, run the following commands.

1. Reset the password for the ubuntu account::

     sudo passwd ubuntu

and set it to something you'll remember.

2. Next, install R and the gdebi tool::

     sudo apt-get update && sudo apt-get install gdebi-core r-base

3. Download & install RStudio Server::
   
     wget https://download2.rstudio.org/rstudio-server-0.99.891-amd64.deb
     sudo gdebi -n rstudio-server-0.99.891-amd64.deb

4. Finally, go to 'http://' + your hostname + ':8787' in a browser,
eg. ::

   http://ec2-XX-YY-33-165.us-west-1.compute.amazonaws.com:8787/

and log into RStudio with username 'ubuntu' and password whatever you set
it to.

Voila!

.. @CTB demonstrate graphing, etc.
.. revisiting what we did...

---
published: true
title: Installing R Shiny On CentOS server
layout: post
tags: [Unix, R]
modified: 2013-04-16 
image:
         feature: abstract-5.jpg
comment: true
read-time: false
---

In the last four months, I worked to develop a web application with shiny server to analyze with the _Kernel density estimation_ the density of TV viewers in Tunisia during the prime time.

I will describle below the steps of the installation that will help you if you need to use CentOS 32 bits or 64 bits.


# I’m a root user  !

Through my experience , I can advise you to install these development libraries first

         yum install libssl-dev
         yum install openssl-devel

Install Node.js from the official web site See related article here

      cd /opt
      wget http://nodejs.org/dist/latest/node-v0.10.5.tar.gz
      tar -xvf node-v0.10.5.tar.gz
      cd node-v0.10.5
      ./configure && make && sudo make install


Now, you can install R  but before, this  you make sure to install _EPEL_ repos  

      wget http://rpms.famillecollet.com/enterprise/remi-release-6.rpm
      sudo rpm -Uvh remi-release-6*.rpm epel-release-6*.rpm
      ls -1 /etc/yum.repos.d/epel* /etc/yum.repos.d/remi.repo
      /etc/yum.repos.d/epel.repo
      /etc/yum.repos.d/epel-testing.repo
      /etc/yum.repos.d/remi.repo

with this command  you can see all installed repos and then change enabled from 1 to 0

         vi /etc/yum.repos.d/

Then you are ready to install R and Rstudio server.

    yum install -y R-base 
    cd /tmp/
    wget http://download2.rstudio.org/rstudio-server-0.97
    .449-x86_64.rpm
    yum install --nogpgcheck rstudio-server-0.97.449-x86_64.rpm

to Install npm

    yum install npm

 Install Shiny server with npm command 

    npm install -g shiny-server

After finishing the installation , you can configure the starting method of R studio

    p –R config/upstart/shiny-server.conf /etc/init/

You are ready to start shiny server now !

    start shiny-server

Finally, I installed packages using the terminal not RStudio server because it's simplify the setup of UNIX File Permissions,but you can use as well the Rstudio interface.

    u - -c "R -e \"install.packages('dbconnect',repos='http://cran.r-project.org/')\""

That's it ! please let me know if it was helpful for you  .


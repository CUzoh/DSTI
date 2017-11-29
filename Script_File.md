The scripts below installs R, RStudio Server, Shiny and Shiny Server (for Web Visualization) and also creates a new user with password for accessing R Studio after installation. You can add more users.

*Check https://www.rstudio.com/products/rstudio/download-server for the latest versions of RStudio Server and Shiny Server and update the script accordingly.*



```
#!/bin/bash
#install R
yum install -y R

#install RStudio-Server 1.1.383 (2017-11-25)
wget https://download2.rstudio.org/rstudio-server-rhel-1.1.383-x86_64.rpm 
yum install -y --nogpgcheck rstudio-server-rhel-1.1.383-x86_64.rpm
rm rstudio-server-rhel-1.1.383-x86_64.rpm

#install shiny and shiny-server (2017-11-25)
R -e "install.packages('shiny', repos='http://cran.rstudio.com/')"
wget https://download3.rstudio.org/centos5.9/x86_64/shiny-server-1.5.5.872-rh5-x86_64.rpm
yum install -y --nogpgcheck shiny-server-1.5.5.872-rh5-x86_64.rpm
rm shiny-server-1.5.5.872-rh5-x86_64.rpm

#add user(s)
useradd firstuser
echo firstuser:password | mydefpword
```


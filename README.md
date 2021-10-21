# replicant
Script that make simple system monitoring and make html page.

## How work?

The need for monitoring a VPS made me create this script;
It monitors the following items that I think are important:

* System info: distribuition, kernel, total packages, Uptime
* Ports services [open] or [down]
* Disk usage
* Packages: Installed, removed and updated (today)
* Top 10 logs size

Every script is executed and outputs to a '.html file', which you can view in your local network or even over the internet.
For internet viewing it is recommended authentication by apache or nginx.

## Note
Replicant does not work with more than one server, it was created this way for simple monitoring. Maybe in the future we can add support for monitoring more than one server

### Example 1
![screen 1](screen/page1.png)

### Example 2
![screen 2](screen/page2.png)

### Responsive mode
![screen 3](screen/page3.png)

## Install and test

### Clone repo
`git clone https://github.com/slackjeff/replicant/`

### Enter directory repo and give permission on script.
`cd replicant && chmod u+x replicant`

### Copy script to /usr/local/bin/
`sudo cp replicant /usr/local/bin/`

### Create directory on /var/www/html
`mkdir -v /var/www/html/replicant`

### Put on cron
`* * * * * /usr/local/bin/replicant > /var/www/html/index.html`

## If you need authentication on apache
### Install apache2-utils
`sudo apt-get install apache2-utils`

### Create user and password for apache
`htpasswd -B -c /etc/apache2/.htpasswd YourUsername`

### Add on /etc/apache2/apache2.conf
`
<Directory "/var/www/html/replicant/">
    AuthType Basic
    AuthName "Restricted Content"
    AuthUserFile /etc/apache2/.htpasswd
    Require valid-user
</Directory>
`

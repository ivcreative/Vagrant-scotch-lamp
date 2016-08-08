# Vagrant-scotch-lamp
My personal modified Vagrant lamp file based on scotch box

##This version includes:

## My Features

- Multisite settings ready
- Folder db for database
- Mysql dump backups on each provision by date

## Quick setup

- Add projects on vagrant file at line 25 each project should be added with quots, example: "project1.dev" "yourdomain.dev" "projectnamex.dev" and so on.
- After adding a project run vagrant up then vagrant provision so it creats the necesary folders.
- Add your new project domain to the host list of your system, on a windows machine this is located at C:\Windows\System32\drivers\etc\hosts remeber this file can only be edited by admin or root. Host should start with the box ip 192.168.33.10 then your project domain an example of how it should look:
 
```192.168.33.10 project1.dev
192.168.33.10 domainxyz.dev
192.168.33.10 mydomainname.dev
192.168.33.10 project201.dev```


### System Stuff

- Ubuntu 14.04 LTS (Trusty Tahr)
- PHP 5.6
- Ruby 2.2.x
- Vim
- Git
- cURL
- GD and Imagick
- Composer
- Beanstalkd
- Node
- NPM
- Mcrypt

### Database Stuff
- MySQL
- PostgreSQL
- SQLite

### Caching Stuff

- Redis
- Memcache and Memcached

### Node Stuff

- Grunt
- Bower
- Yeoman
- Gulp
- Browsersync
- PM2

### Laravel Stuff

- Laravel Installer
- Laravel Envoy
- Blackfire Profiler

### Other Useful Stuff

- No Internet connection required
- PHP Errors turned on
- Laravel and WordPress ready
- Operating System agnostic
- Goodbye XAMPP / WAMP
- New Vagrant version? Update worry free. ScotchBox is very reliable with a lesser chance of breaking with various updates
- Super easy database access and control
- [Virtual host ready](https://scotch.io/bar-talk/announcing-scotch-box-2-0-our-dead-simple-vagrant-lamp-stack-improved#multiple-domains-(virtual-hosts))
- PHP short tags turned on
- H5BP’s server configs
- MIT License



## Get Started

* Download and Install [Vagrant][3]
* Download and Install [VirtualBox][4]
* Clone the Scotch Box [GitHub Repository](https://github.com/ivcreative/Vagrant-scotch-lamp.git)
* Run ``` vagrant up ```
* Access Your Project at  [http://192.168.33.10/][14]

## Basic Vagrant Commands


### Start or resume your server
```bash
vagrant up
```

### Pause your server
```bash
vagrant suspend
```

### Delete your server
```bash
vagrant destroy
```

### SSH into your server
```bash
vagrant ssh
```



## Database Access

### MySQL 

- Hostname: localhost or 127.0.0.1
- Username: root
- Password: root
- Database: scotchbox

### PostgreSQL

- Hostname: localhost or 127.0.0.1
- Username: root
- Password: root
- Database: scotchbox
- Port: 5432


### MongoDB

- Hostname: localhost
- Database: scotchbox
- Port: 27017


## SSH Access

- Hostname: 127.0.0.1:2222
- Username: vagrant
- Password: vagrant

## Mailcatcher

Just do:

```
vagrant ssh
mailcatcher --http-ip=0.0.0.0
```

Then visit:

```
http://192.168.33.10:1080
```


## Updating the Box

Although not necessary, if you want to check for updates, just type:

```bash
vagrant box outdated
```

It will tell you if you are running the latest version or not, of the box. If it says you aren't, simply run:

```bash
vagrant box update
```


## Setting a Hostname

If you're like me, you prefer to develop at a domain name versus an IP address. If you want to get rid of the some-what ugly IP address, just add a record like the following example to your computer's host file.

```bash
192.168.33.10 whatever-i-want.local
```

Or if you want "www" to work as well, do:

```bash
192.168.33.10 whatever-i-want.local www.whatever-i-want.local
```

Technically you could also use a Vagrant Plugin like [Vagrant Hostmanager][15] to automatically update your host file when you run Vagrant Up. However, the purpose of Scotch Box is to have as little dependencies as possible so that it's always working when you run "vagrant up".


## Configuration

You may want to change some of the out-of-the-box configurations for
the various parts that come with Scotch Box.  To do so, `vagrant ssh`
into the box, and edit the appropriate file.  For example, to change
PHP settings:

    vagrant ssh
    sudo vim /etc/php5/apache2/conf.d/user.ini

Note that the changes that you make will be for the current running
Scotch Box only.  If you `vagrant destroy` and then `vagrant up` your
box again, these manual configuration changes will be lost.

If you prefer to automate your configuration changes so that you can
destroy and re-create boxes as needed, Vagrant allows you to create a
"provision script" that runs as part of `vagrant up`.  See the
[Vagrant
documentation](https://docs.vagrantup.com/v2/getting-started/provisioning.html)
for notes.  For example, you could add the following line to your
Vagrantfile under the `config.vm.hostname = "scotchbox"` line:

    config.vm.provision :shell, path: "bootstrap.sh"

and then create `bootstrap.sh` with the following content in the same
directory as the Vagrantfile:

    #!/bin/bash
    # Disable Zend OPcache
    sed -i 's/;opcache.enable=0/opcache.enable=0/g' /etc/php5/apache2/php.ini

This script will be run each time you `vagrant up`, and it can be run
on an already-up box using `vagrant provision`.

## PHP7 Install Instructions

```
sudo apt-get update
sudo add-apt-repository ppa:ondrej/php
sudo apt-get install php7.0
sudo apt-get update
sudo apt-get install php7.0-mysql libapache2-mod-php7.0
sudo a2dismod php5
sudo a2enmod php7.0
sudo apachectl restart
```


## The MIT License (MIT)

Copyright (c) 2014-2015 Nicholas Cerminara, scotch.io, LLC

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.



 [1]: https://github.com/MiniCodeMonkey/Vagrant-LAMP-Stack
 [2]: http://scotch.io/tutorials/get-vagrant-up-and-running-in-no-time
 [3]: https://www.vagrantup.com/downloads.html
 [4]: https://www.virtualbox.org/wiki/Downloads
 [5]: http://www.sequelpro.com/
 [6]: http://www.navicat.com/
 [7]: http://github.com/scotch-io
 [8]: http://twitter.com/scotch_io
 [9]: https://github.com/smdahlen/vagrant-hostmanager
 [10]: http://scotch.io/tutorials/sharing-your-virtual-machine-on-the-web-with-vagrant-share
 [11]: http://scotch.io/tutorials/php/getting-started-with-laravel-homestead
 [12]: https://www.vagrantup.com/downloads.html
 [13]: https://www.virtualbox.org/wiki/Downloads
 [14]: http://192.168.33.10/
 [15]: https://github.com/smdahlen/vagrant-hostmanager
 [16]: http://box.scotch.io
 [17]: http://scotch.io/bar-talk/introducing-scotch-box-a-vagrant-lamp-stack-that-just-works

# -*- mode: ruby -*-
# vi: set ft=ruby :

## File prepared by Miguel Quintero for Subject Matter Dev Team

Vagrant.configure("2") do |config|

    config.vm.box = "scotch/box"
    config.vm.network "private_network", ip: "192.168.33.10"
    config.vm.hostname = "scotchbox"
    config.vm.synced_folder ".", "/var/www", :nfs => { :mount_options => ["dmode=777","fmode=666"] }

        config.vm.provider "virtualbox" do |v|
            v.memory = 2048
            v.cpus = 2
        end    


    config.vm.provision "shell", inline: <<-SHELL

        ## Only thing you probably really care about is right here, change the clientdomain.dev to real clients projects to add more just add a space "projects.dev" remeber after adding each you need to run
        ## vagrant provision and also add on your /etc/host the new projects example 192.168.33.10 projectname.dev
        ## When creating a client environment name the database as same as your clientproject.dev in order to allow the script below create backups of the dev project database.
        
        DOMAINS=("database.local" "clientdomain1.dev" "clientdomain2.dev")

        echo "TEAM SUBJECT MATTER VAGRANT POWER O YEA!!!! \n"
        echo "\n"

        echo ".######..######...####...##...##...........####...##..##..#####...######..######...####...######..........##...##...####...######..######..######..#####.."
        echo "...##....##......##..##..###.###..........##......##..##..##..##......##..##......##..##....##............###.###..##..##....##......##....##......##..##."
        echo "...##....####....######..##.#.##...........####...##..##..#####.......##..####....##........##............##.#.##..######....##......##....####....#####.."
        echo "...##....##......##..##..##...##..............##..##..##..##..##..##..##..##......##..##....##............##...##..##..##....##......##....##......##..##."
        echo "...##....######..##..##..##...##...........####....####...#####....####...######...####.....##............##...##..##..##....##......##....######..##..##."
        echo ".........................................................................................................................................................."
        echo "\n "

        ## Loop through all sites
        for ((i=0; i < ${#DOMAINS[@]}; i++)); do

            ## Current Domain
            DOMAIN=${DOMAINS[$i]}

            echo "Creating directory for $DOMAIN..."
            sudo mkdir -p /var/www/$DOMAIN/public
            sudo mkdir -p /var/www/$DOMAIN/db


            echo "Database backup for $DOMAIN"
            sudo mysqldump -u root -proot $DOMAIN > /var/www/$DOMAIN/db/$DOMAIN_$(date +"%Y-%m-%d").sql

            echo "Creating vhost config for $DOMAIN..."
            sudo cp /etc/apache2/sites-available/scotchbox.local.conf /etc/apache2/sites-available/$DOMAIN.conf

            echo "Updating vhost config for $DOMAIN..."
            sudo sed -i s,scotchbox.local,$DOMAIN,g /etc/apache2/sites-available/$DOMAIN.conf
            sudo sed -i s,/var/www/public,/var/www/$DOMAIN/public,g /etc/apache2/sites-available/$DOMAIN.conf

            echo "Enabling $DOMAIN. Will probably tell you to restart Apache..."
            sudo a2ensite $DOMAIN.conf

            



        done

        echo "So let's restart apache..."
        sudo service apache2 restart

        echo "Restart Mysql"
        sudo service mysql restart

    SHELL

    

end

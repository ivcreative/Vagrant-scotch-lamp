# -*- mode: ruby -*-
# vi: set ft=ruby :

## File prepared by Miguel Quintero for Subject Matter Dev Team

Vagrant.configure("2") do |config|

    config.vm.box = "scotch/box"
    config.vm.network "private_network", ip: "192.168.33.10"
    config.vm.hostname = "scotchbox"
    config.vm.synced_folder ".", "/var/www", :nfs => { :mount_options => ["dmode=777","fmode=666"] }

    config.vm.provider :virtualbox do |v|
        v.customize ["modifyvm", :id, "--memory", 2048]
    end


    config.vm.provision "shell", inline: <<-SHELL

        ## Only thing you probably really care about is right here
        DOMAINS=("database.dev" "shadygroveortho.dev" "buildingtrades.dev" "mosaic.dev" "silverafilm.dev" "carpenters.dev" "nccmp.dev" "nabtutheme.dev" "mosaicinternal.dev" "diverscope.dev")

        echo "MOSAIC VAGRANT POWER O YEA!!!! \n"
        echo "\n"

        echo '    
  SSSSSSSSSSSSSSS              AAA               DDDDDDDDDDDDD      EEEEEEEEEEEEEEEEEEEEEE   SSSSSSSSSSSSSSS 
 SS:::::::::::::::S            A:::A              D::::::::::::DDD   E::::::::::::::::::::E SS:::::::::::::::S
S:::::SSSSSS::::::S           A:::::A             D:::::::::::::::DD E::::::::::::::::::::ES:::::SSSSSS::::::S
S:::::S     SSSSSSS          A:::::::A            DDD:::::DDDDD:::::DEE::::::EEEEEEEEE::::ES:::::S     SSSSSSS
S:::::S                     A:::::::::A             D:::::D    D:::::D E:::::E       EEEEEES:::::S            
S:::::S                    A:::::A:::::A            D:::::D     D:::::DE:::::E             S:::::S            
 S::::SSSS                A:::::A A:::::A           D:::::D     D:::::DE::::::EEEEEEEEEE    S::::SSSS         
  SS::::::SSSSS          A:::::A   A:::::A          D:::::D     D:::::DE:::::::::::::::E     SS::::::SSSSS    
    SSS::::::::SS       A:::::A     A:::::A         D:::::D     D:::::DE:::::::::::::::E       SSS::::::::SS  
       SSSSSS::::S     A:::::AAAAAAAAA:::::A        D:::::D     D:::::DE::::::EEEEEEEEEE          SSSSSS::::S 
            S:::::S   A:::::::::::::::::::::A       D:::::D     D:::::DE:::::E                         S:::::S
            S:::::S  A:::::AAAAAAAAAAAAA:::::A      D:::::D    D:::::D E:::::E       EEEEEE            S:::::S
SSSSSSS     S:::::S A:::::A             A:::::A   DDD:::::DDDDD:::::DEE::::::EEEEEEEE:::::ESSSSSSS     S:::::S
S::::::SSSSSS:::::SA:::::A               A:::::A  D:::::::::::::::DD E::::::::::::::::::::ES::::::SSSSSS:::::S
S:::::::::::::::SSA:::::A                 A:::::A D::::::::::::DDD   E::::::::::::::::::::ES:::::::::::::::SS 
 SSSSSSSSSSSSSSS AAAAAAA                   AAAAAAADDDDDDDDDDDDD      EEEEEEEEEEEEEEEEEEEEEE SSSSSSSSSSSSSSS 
                 ';

		echo "\n "

        echo 'echo "upload_max_filesize = 100M" >> /etc/php5/apache2/conf.d/user.ini' | sudo -s
        echo 'echo "post_max_size = 100M" >> /etc/php5/apache2/conf.d/user.ini' | sudo -s

        echo "\n "
        
        ## Loop through all sites
        for ((i=0; i < ${#DOMAINS[@]}; i++)); do

            ## Current Domain
            DOMAIN=${DOMAINS[$i]}

            echo "Creating directory for $DOMAIN..."
            sudo mkdir -p /var/www/$DOMAIN/public
            sudo mkdir -p /var/www/$DOMAIN/db

            ## echo "create empty dump"
            ## touch "/var/www/$DOMAIN/db/dump_$DOMAIN.sql"

            echo "Database backup for $DOMAIN"
            sudo mysqldump -u root -proot $DOMAIN > /var/www/$DOMAIN/db/$DOMAIN-$(date +%Y-%m-%d).sql

            echo "Creating vhost config for $DOMAIN..."
            sudo cp /etc/apache2/sites-available/scotchbox.local.conf /etc/apache2/sites-available/$DOMAIN.conf

            echo "Updating vhost config for $DOMAIN..."
            sudo sed -i s,scotchbox.local,$DOMAIN,g /etc/apache2/sites-available/$DOMAIN.conf
            sudo sed -i s,/var/www/public,/var/www/$DOMAIN/public,g /etc/apache2/sites-available/$DOMAIN.conf

            echo "Enabling $DOMAIN. Will probably tell you to restart Apache..."
            sudo a2ensite $DOMAIN.conf

            echo "So let's restart apache..."
            sudo service apache2 restart



        done

    SHELL

end

# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure(2) do |config|

  config.vm.box = "puphpet/debian75-x32"
  config.vm.network "private_network", ip: "192.168.33.10"
  config.vm.synced_folder ".", "/home/vagrant", :mount_options => ["dmode=777", "fmode=666"]
  config.vm.provision "shell", inline: <<-SHELL
    sudo apt-get update
    sudo apt-get install -y nginx php5-fpm php-pear php5-imap
    sudo rm /etc/nginx/sites-enabled/default
    sudo printf '%s\n' 'server {' 'root /home/vagrant/web;' 'index index.php index.html index.htm;' 'location / {' 'try_files $uri $uri/ /index.php?$args ;' '}' 'location ~ \.php$ {' 'fastcgi_split_path_info ^(.+\.php)(/.+)$;' 'fastcgi_pass unix:/var/run/php5-fpm.sock;' 'fastcgi_index index.php;' 'include fastcgi_params;' '}' '}' >> /etc/nginx/sites-enabled/default
    sudo service nginx start
  SHELL
end

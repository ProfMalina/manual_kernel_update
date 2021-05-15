# HW1

 - Установил Packer (vagrant и vmbox установлены до занятий)

`wget https://releases.hashicorp.com/packer/1.4.4/packer_1.4.4_linux_amd64.zip`

`unzip packer_1.4.4_linux_amd64.zip`

`sudo mv packer /usr/local/bin/packer`

`sudo chmod +x /usr/local/bin/packer`

`rm packer_1.4.4_linux_amd64.zip`

 - Сделал fork необходимого репозитория и склонировал на рабочую станцию

`git clone git@github.com:ProfMalina/manual_kernel_update.git`

`cd manual_kernel_update`

 - Выполнил действия согласно заданию

`vagrant up`

`vagrant ssh`

`sudo yum install -y http://www.elrepo.org/elrepo-release-7.0-3.el7.elrepo.noarch.rpm`

`sudo yum --enablerepo elrepo-kernel install kernel-ml -y`

`sudo grub2-mkconfig -o /boot/grub2/grub.cfg`

`sudo grub2-set-default 0`

`sudo reboot`

`vagrant ssh`

 - После перезапуска проверил успешность выполненых действий

`uname -r`

 - Изменил файл centos.json, добавил существующий образ который скачивается не 4 часа затем собрал образ

`packer build centos.json`

 - Провёл тестирование

`vagrant box add --name centos-7-5 centos-7.9.2009-kernel-5-x86_64-Minimal.box`

`vagrant box list`

`vagrant init centos-7-5`

`vagrant box remove centos-7-5`

 - Опубликовал свой образ, изменил его приватность на видимый

`vagrant cloud auth login`

`vagrant cloud publish --release ProfMalina/centos-7-5 1.0 virtualbox centos-7.9.2009-kernel-5-x86_64-Minimal.box`

 - Добавил свой образ в Vagrantfile и проверил работоспособность

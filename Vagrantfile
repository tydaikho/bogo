# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure(2) do |config|
  config.vm.define "ubuntu-14.04" do |ubuntu|
    ubuntu.vm.box = "ubuntu/trusty64"

script = <<SCRIPT
CORE_DEPS="valac libgtk2.0-dev libgtk-3-dev python3-dev python3-pip"
TEST_DEPS="openbox xvfb xdotool python-dogtail org.gnome.desktop.interface"
TEST_APPS="vim-gtk geany libreoffice-writer terminator inkscape"
UTILS="byobu"

add-apt-repository ppa:vala-team/ppa
apt-get update
apt-get install -y $CORE_DEPS $TEST_DEPS $TEST_APPS $UTILS

pip3 install bogo
SCRIPT
    
    ubuntu.vm.provision "shell", inline: script
  end

  config.vm.define "fedora-21" do |fedora|
    fedora.vm.box = "hansode/fedora-21-server-x86_64"

script = <<SCRIPT
timedatectl set-local-rtc 0

CORE_DEPS="vala gtk2-devel gtk3-devel python3-devel"
TEST_DEPS="openbox xdotool dbus-x11 xorg-x11-server-Xvfb"
TEST_APPS="gvim geany libreoffice-writer inkscape terminator"
UTILS="byobu psmisc"

yum install -y $CORE_DEPS $TEST_DEPS $TEST_APPS $UTILS
yes | pip3 install bogo
SCRIPT

    fedora.vm.provision "shell", inline: script
  end

  config.vm.provider "virtualbox" do |vb|
    # Display the VirtualBox GUI when booting the machine
    vb.gui = true
  
    # # Customize the amount of memory on the VM:
    # vb.memory = "1024"
  end
end

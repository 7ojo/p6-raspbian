Getting Started
===============

Initial Setup and Configuration
-------------------------------

Assuming that you have latest Raspbian installed and when this was written it was `stretch`.

#. Keyboard Layout::

       $ sudo dpkg-reconfigure keyboard-configuration
       $ cat /etc/default/keyboard
       
       # KEYBOARD CONFIGURATION FILE
       
       # Consult the keyboard(5) manual page.
       
       XKBMODEL="applealu_iso"
       XKBLAYOUT="fi"
       XKBVARIANT="mac"
       XKBOPTIONS="lv3:lalt_switch"
       
       BACKSPACE="guess"
       
       $ sudo reboot

#. WiFi Configuration::

       $ sudo iwlist wlan0 scan
       $ sudo su
       $ sudo wpa_passphrase "<SSID>" "<PASSWORD>" >> /etc/wpa_supplicant/wpa_supplicant.conf

#. Installing Rakudo Perl 6 from `testing`
    
    Stable version of Raspbian has pretty outdated version of Rakudo Perl 6 so here's instructions for installing newer from testing::
    
        $ sudo apt-get install vim
        $ sudo vim /etc/apt/sources.d/testing.list 
        deb http://mirrordirector.raspbian.org/raspbian/ testing main contrib rpi

        $ sudo vim /etc/apt/preferences.d/testing
        Package: *
        Pin: release a=testing
        Pin-Priority: 100

        $ sudo apt-get update
        $ sudo apt-cache policy rakudo # Take the version number here e.g. 2017.06-1
        $ sudo apt-get install -t testing rakudo

#. Install `zef` Package Management Tool::

       $ sudo apt-get install git
       $ git clone https://github.com/ugexe/zef.git
       $ cd zef
       $ perl6 -Ilib bin/zef install .
       $ echo 'PATH=$PATH:/home/pi/.perl6/bin' >> ~/.bashrc
       $ source ~/.bashrc

#. Testing Rakudo Perl6 REPL
   
   Getting the history functionality and such to work we need to install e.g. `Readline`::
   
       $ sudo apt-get install libreadline-dev
       $ zef install Readline
       $ perl6


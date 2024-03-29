## Install VirtualBox Fedora

    sudo dnf -y install @development-tools
    sudo dnf -y install kernel-headers kernel-devel dkms elfutils-libelf-devel qt5-qtx11extras
    cat <<EOF | sudo tee /etc/yum.repos.d/virtualbox.repo
    [virtualbox]
    name=Fedora $releasever - $basearch - VirtualBox
    baseurl=http://download.virtualbox.org/virtualbox/rpm/fedora/36/\$basearch
    enabled=1
    gpgcheck=1
    repo_gpgcheck=1
    gpgkey=https://www.virtualbox.org/download/oracle_vbox.asc
    EOF
    sudo dnf search virtualbox
    sudo dnf install VirtualBox-7.0
    sudo usermod -a -G vboxusers $USER

## Create Tap interface

    sudo dnf install tunctl
    sudo tunctl -u rifan
    sudo ifconfig tap0 10.123.1.1 netmask 255.255.255.0 up
    echo 1 > /proc/sys/net/ipv4/ip_forward

## Config Iptables

    sudo dnf install iptables-services
    sudo systemctl enable iptables
    sudo systemctl start iptables
    sudo systemctl status iptables
    iptables -t nat -A POSTROUTING -o wlp5s0 -j MASQUERADE
    iptables -A FORWARD -i tap0 -j ACCEPT
    iptables -A INPUT -i tap0 -j ACCEPT
    /sbin/iptables-save > /etc/sysconfig/iptables
    cat /etc/sysconfig/iptables

### Host Prohibited

    sudo -i
    nano /etc/sysconfig/iptables
    iptables-restore < /etc/sysconfig/iptables
    iptables -L

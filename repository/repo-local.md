## Create Local Repository

Config apt-mirror

    apt install apt-mirror
    nano /etc/apt/mirror.list
    set base path /home/tkj/fileweb
    mkdir /home/tkj/fileweb/debian10
        deb [arch=amd64] http://kartolo.sby.datautama.net.id/debian/ buster main contrib non-free
        deb-src [arch=amd64] http://kartolo.sby.datautama.net.id/debian/ buster main contrib non-free

atur ServerRoot Apache2
/home/tkj/fileweb/
atur apache2.conf

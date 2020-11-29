
#!/bin/bash
# Setup new Raspberry Pi
if [ "$#" -ne 2 ]; then
    echo "Illegal number of parameters. Expected hostname and last node of ip"
fi

echo 'Update Rasbian'
sudo apt update && apt full-upgrade -y

echo 'Update eeprom rpi firmware'
sudo rpi-eeprom-update -a

hostname $1

locale-gen --purge en_US.UTF-8
# Configure timezone and locale
echo "America/Chicago" > /etc/timezone && \
    dpkg-reconfigure -f noninteractive tzdata && \
    sed -i -e 's/# en_US.UTF-8 UTF-8/en_US.UTF-8 UTF-8/' /etc/locale.gen && \
    echo 'LANG="en_US.UTF-8 "'>/etc/default/locale && \
    dpkg-reconfigure --frontend=noninteractive locales && \
    update-locale LANG=en_US.UTF-8


sudo cp /etc/dhcpcd.conf /etc/dhcpcd.conf.bak
sudo cat >> /etc/dhcpcd.conf << EOF
interface eth0
static ip_address=192.168.1.$2/24
static routers=192.168.1.1
static domain_name_servers=192.168.1.1 8.8.8.8
EOF
echo /etc/dhcpcd.conf

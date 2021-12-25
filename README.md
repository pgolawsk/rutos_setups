# rutos_setups

RutOS automated setups through Ansible.

Author Pawel Golawski <pawel.golawski@2com.pl>

## Contents

This repository contains Ansible scripts for RutOS devices to recreate setup on new device or after firmware update.

* ```playbooks/rutx11_setup.yml``` - this is recreate setup script after firmware update. It re-installs:
  * ```Iperf3``` - network speed testing tool;
  * ```HAProxy``` - loadbalancer for network services; uses pre-existing ```/etc/haproxy.cfg``` setup file;
  ***
  (__NOT working for firmware 07.00 and above due to change LUCI to VUCI__)
  * ```CollectD``` - collecting statistics localy of cpu, memory, disk IO, ping and many others; uses pre-esisting ```/etc/collectd.conf``` file;
    * it includes specific ```exec``` mod for customized stats for GSM/LTE signal strenght and device temperatre recordings;
  * ```LUCI-statistics``` - displaying CollectD statistics on web interface; uses pre-existing ```/etc/config/luci_statistics``` setup file;
    * it includes specific ```exec``` LUA script to display above data (```/usr/lib/lua/luci/statistics/rrdtool/definitions/exec.lua```);
  ***
  * ```VNStat``` - gathering summary data total transfered data by interface by day/month, ... (to monitor use of GSM/LTE data plans); uses pre-existing ```/etc/config/vnstat``` and ```/etc/vnstat.conf``` setup files; use command line tool ```vnstat``` to display data;
  * ```BandwidthD``` - gathering by IP/host summary stats of data transferred by device by day/week/month; uses pre-existing ```/etc/config/bandwidthd``` and ```/etc/bandwidthd.conf``` setup files;
  * update (or create if does not exists) ```/etc/sysupgrade.conf``` file to presere other mentioned above setup files for future firmware upgrades (so current setup is not lost post the upgrade)

## Usage

Before running it please create valid inventory file - see example in ```inventory_example.ini```.

Example of using specific playbook.

```bash
ansible-playbook -i my_inventory_file.ini playbooks/rutx11_setup.yml
```

## My future plans for playbooks (TODO)

* [ ] ```rutx11_setup.yml``` - to split it into a few scripts for clean device, recreate only and divide scripts into some components for different packages - like collectd, bandwidthd, vnstat, ...

[//]: # (None at the moment)

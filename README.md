# rutos_setups
RutOS automated setups through Ansible.

Author Pawel Golawski <pawel.golawski@2com.pl>

## Contents
This repository contains Ansible scripts for RutOS devices to recreate setup on new device or after firmware update.

* ```playbooks/rutx11_setup.yml``` - this is recreate script for the setupafter firmware update. It contains:
  * ```Iperf3``` - network speed testing tool
  * ```HAProxy``` - loadbalancer for network services
  * ```CollectD``` - collecting statistics localy of cpu, memory, disk IO, ping and many others
    * it includes specific ```exec``` mod for customized stats for GSM/LTE signal strenght and device temperatre recordings

(to be added soon)
  * ```LUCI-statistics``` - displaying CollectD statistics on web interface
  * ```VNStat``` - gathering summary data total transfered data by interface by day/month, .. (to monitor use of GSM/LTE data plans)
  * ```BandwidthD``` - gathering by IP/host summary stats of data transferred by device by day/week/month.

## Usage
Before running it please create valid inventory file - see example in ```inventory_example.ini```.

Example of using specific playbook.

```bash
ansible-playbook -i my_inventory_file.ini playbooks/rutx11_setup.yml
```

## My future plans for playbooks (TODO)

- [ ] ```rutx11_setup.yml``` - to split it into a few scripts for clean device, recreate only and divide scripts into some components for different packages - like collectd, badwithd, vnstat, ...

[//]: # (None at the moment)
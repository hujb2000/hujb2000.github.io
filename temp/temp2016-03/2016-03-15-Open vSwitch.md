---
---
layout: post
title:  "Open vSwitch"
date:   2016-03-15 13:35:30
categories: allen.hu update
---

[Open vSwitch](http://openvswitch.org/)

wget http://openvswitch.org/releases/openvswitch-2.5.0.tar.gz
./configure
make
make install


Q:
ovs-vsctl: unix:/usr/local/var/run/openvswitch/db.sock: database connection failed (No such file or directory)

A:
ovsdb-server --remote=punix:/usr/local/var/run/openvswitch/db.sock \
                     --remote=db:Open_vSwitch,Open_vSwitch,manager_options \
                     --private-key=db:Open_vSwitch,SSL,private_key \
                     --certificate=db:Open_vSwitch,SSL,certificate \
                     --bootstrap-ca-cert=db:Open_vSwitch,SSL,ca_cert \
                     --pidfile --detach
ovs-vsctl --no-wait init
ovs-vswitchd --pidfile --detach

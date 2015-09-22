## Proble Statement

While building [Griggi](griggi.com), we have this unique problem. We would like to share the bandwidth **equally** among all the connected guests. 

This problem hasn't been solved so far. This is technically called **traffic shaping**. There are ways to limit the overall bandwidth for guests to, lets say, 10 Mbps; or there are ways to limit every user bandwidth to, lets say, 1 Mbps; but there is no way to dynamically calculate the uplink speed & divide it among the clients connected. 


### Why we need this 

While in general, the bandwidth available is divided equally among all users, some user can still hog bandwidth & others will get reduced speed (like running a Youtube video in a public hotspot). 

While pre-fixing rate of the user to a pre-defined value (like 1 Mbps) can solve this problem, but it is far from optimal. If the uplink speed is 10 Mbps & there is just 1 user, why should he live with just 1 Mbps speed !

The most popular way to do traffic shaping is by using **tc** & **iptables**. Details at [Network Traffic Control in Openwrt](http://wiki.openwrt.org/doc/howto/packet.scheduler/packet.scheduler). 

An example openwrt configuration using tc command can be seen [here](http://wiki.openwrt.org/doc/howto/packet.scheduler/packet.scheduler.example2)

But the way still does not provide an ideal scenario. Ideally, this should be achievable through a kernel module. 

#### Setup - Openwrt & Openwrt SDK

**prerequisite - you need a linux machine**

1. Download Virtual Box for linux. 
2. Follow steps [here](http://wiki.openwrt.org/doc/howto/virtualbox) to setup openwrt inside virtual box. Also, setup a client in virtual box (as explained in the last part) & make sure it gets internet through the openwrt so that you have a client ready to test.
3. Download [Openwrt SDK for linux](https://downloads.openwrt.org/barrier_breaker/14.07/x86/generic/OpenWrt-SDK-x86-for-linux-x86_64-gcc-4.8-linaro_uClibc-0.9.33.2.tar.bz2). Using this SDK, you can build Openwrt package that you can install in your Virtualbox Openwrt. References - [helloworld package building](http://www.electronicsfaq.com/2015/04/installing-and-using-openwrt-sdk-on.html), [official doc on creating package](http://wiki.openwrt.org/doc/devel/packages)

Another option is - we are using [Wifidog](https://github.com/wifidog) for letting people share their Wifi. It is largely responsible to show a captive portal in which guests would need to log in to start using the Wifi hotspot. If wifidog code be changed to pre-build this feature, that would be fine too. 

To change wifidog, simply clone it inside package directory in SDK & after code change, do `make package/wifidog/compile` to generate the modified ipk, transfer it to openwrt & install. 

### How to contribute 

Create an issue with the way you intend to solve (or if you have any problem). One of us will respond to it ASAP. 

You could go ahead, fork this repo & send pull request when done. 

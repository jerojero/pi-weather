# pi-weather
Repo to easily modify front-end of raspberry-pi local weather visualization, forecast (eventually), *and* analytics server. Mathematical! (*maybe*)

[Consider using flask in the future](http://www.raspberrypi-spy.co.uk/2017/07/create-a-basic-python-web-server-with-flask/)

## How to replicate:

* First, choose what sort stack you want
    * Follow [this guide](https://diyhacking.com/raspberry-pi-web-server/) to install apache2, and php5, otherwise known as a [LAMP stack](https://en.wikipedia.org/wiki/LAMP_(software_bundle)). 
    * *Or* **more prefered model:** Just install node.js since we're going to be using it regardless. Either way as long as you can make your pi send an HTML page, it doesn't really matter.
    
    ***See below steps for installing node.js on ARM architecture***

* Give pi static IP, portfoward port 80 from your router (I also recommend port 22 so you can SSH into your pi externally, for development at least)
* If you want, assign a DNS to your external IP. I used [this DNS provider](http://freedns.afraid.org/). Let this serve as me adhering to their desire to post a link to their site on my project!
    * If you forwarded port 22 you can ssh from this URL also, which is handy
* Install node & npm
    * Pi is arm so usual method won't work, follow [this guide](http://weworkweplay.com/play/raspberry-pi-nodejs/) or use the commands listed below
---
## Commands to get started:
```bash
# cd to where you would like the repo directory to be
# git clone this repo
# cd to repo directory
wget http://node-arm.herokuapp.com/node_latest_armhf.deb 
sudo dpkg -i node_latest_armhf.deb
rm node_latest_armhf.deb
npm install # this will install all dependencies listed in package.json &mdash; namely express, pug, particle-api, node scheduler, raspicam node api

# Assuming you don't want to run sudo everytime you launch the server, you'll likely need to redirect a provisional port to port 80 so you can just type in the IP without specifying a port
iptables -t nat -I PREROUTING -p tcp --dport 80 -j REDIRECT --to-port 3000
#   This routes port 3000 to port 80. You'll still need to port-forward to access your server remotely, but otherwise everything in this repo *should* work as it's written for port 3000.

npm run watch # to run the server but automatically restart itself if a file is changed in the directory

# OR

node server.js # to simply run the server as-is
```

* IN THE FUTURE accessing the page should be enough to kick-start all the periodic updates. For right now, you must run `node weather.js` to update anything on the page.
* Todo:
    * Add periodic functions
    * Add photon code to this repository

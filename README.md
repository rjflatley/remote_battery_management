# remote_battery_management
Node-Red and Grafana import files for remote battery management

Step how to setup remote management/data logging/display of your battery and solar status.  This includes a smart BMS, current shunts (coulomb counters), solar MPPT controller and other instruments.  Data is stored in an Influx database with the use of Node-Red and displayed using Grafana.

Install latest version of Raspberry Pi OS from: 
https://www.raspberrypi.org/documentation/installation/installing-images/

Enable SSH on the Raspberry Pi:
https://www.raspberrypi.org/documentation/remote-access/ssh/

Remote log into the Raspberry Pi using your favorite SSH utility (such as putty: https://www.putty.org/)

sudo apt update
sudo apt full-upgrade
curl -sL https://repos.influxdata.com/influxdb.key | sudo apt-key add -
echo "deb https://repos.influxdata.com/debian buster stable" | sudo tee /etc/apt/sources.list.d/influxdb.list
sudo apt update
sudo apt-get install influxdb
sudo systemctl enable --now influxdb
influx
     CREATE USER root WITH PASSWORD 'root' WITH ALL PRIVILEGES
     CREATE DATABASE "battsoc"
     CREATE DATABASE "sfp101evb"
     CREATE DATABASE "tracera12"
     CREATE DATABASE "heartrate"
     CREATE DATABASE "bms"
     exit
bash <(curl -sL https://raw.githubusercontent.com/node-red/linux-installers/master/deb/update-nodejs-and-nodered)
node-red-start
     control c
sudo systemctl enable nodered.service
wget https://dl.grafana.com/oss/release/grafana_7.1.5_armhf.deb
sudo dpkg -i grafana_7.1.5_armhf.deb
sudo /bin/systemctl daemon-reload
sudo /bin/systemctl enable grafana-server
sudo /bin/systemctl start grafana-server
systemctl status grafana-server
    control c

Open the Node-Red interface in your browser on any computer by visiting:
http://Your.IP.Add.ress:1880

Click the burger icon in the top right.
Cut and paste code from here: 
https://raw.githubusercontent.com/rjflatley/remote_battery_management/main/BMS.json

Click the red Deploy icon in the upper right of the page

Open the Grafana interface in your browser on any computer by visiting:
http://Your.IP.Add.ress:3000

(See video for full instructions on setting up databases)
Click on the + (plus symbol) in the upper left of the page.
Select import,
Cut and paste code from here: 
https://raw.githubusercontent.com/rjflatley/remote_battery_management/main/Remote_battery_grafana.json

For EPEver Node-Red setup please visit: 
https://github.com/AdamWelchUK/NodeRedEPEverDashboard

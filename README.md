[![Build Status](https://travis-ci.org/LeadTheSalt/one_home_sensor.svg?branch=master)](https://travis-ci.org/LeadTheSalt/one_home_sensor)
# One Home Sensor

This peace of software reads temperature, pressure and humidity from a BME280 sensor. It then pushes the result to a MongoDB data-base (MongoDB Atlas form my part). 

## Usage 
My setup is as followed :
```
  +-------------+
  | RaspberryPI |    +-------------+    +-------------+ 
  |             |    |  MongoDB    |    |  Phone /    |
  |  one_home_  +--->|  Atlas      +--->|  WebBrowser |
  |     sensor  |    +-------------+    +-------------+
  +-------------+
```
I periodically run it (throught systemd) to store the values. 


## Integration / Instalation
This programe is created and only used/tested/supported in python3. These commande should solve all dificulties. 

```
sudo apt-get update
sudo apt-get install python3-setuptools python3-pip i2c-tools 
```
1. Create cluster on MongoDB Atlas
2. Create connection autorization and user 
3. Create configuration file (see next section)
4. Enable  I2C in raspi-config (5 then P5).
5. Add user to group "i2c" (sudo usermod -a -G i2c leadthesalt)

Finaly the module is installed with pip3.
```
pip3 install one-home-sensor
```

For my part I install the programe with an Ansible rôle. Sure I could create a debian package, but I only use it on my Raspbery Pi that are already managed throught Ansible. 
 
## Configuration file 
```
[MongoDBAtlasConnection]
username = # username set for MongoDB
password = # password set for MongoDB
clusterfqdn = # fqdn to MongoDB server 

[Correction]
temp=-1
```

## Documentations 
https://github.com/pimoroni/bme280-python  
https://github.com/pimoroni/skywriter-hat/issues/4  
https://learn.pimoroni.com/related-products/adafruit-mpl3115a2-i2c-barometric-pressure-altitude-temperature-sensor  
https://docs.mongodb.com/  
# IIoT_module6
IIoT Workshop - Module 6 Case Study 1 Example Code

<img src="https://github.com/JZ2211/IIoT_Case1/assets/100505718/ceb4a08b-a487-4068-b82d-bbf9e66196a6" width="600">

## Steps in a short list:
1.	RPi board should have wifi function. Check your RPi board model using command:
```cat  /proc/cpuinfo```
1.	Verify the system clock synchronization. System clock needs to be synchronized:
   ```timedatectl```
1.	Check the python version. Requires python 3.7 version or above. Please note the double dash:
  ```python --version```  
1.	Install or update setup tools for python:
  ```sudo pip3 install --upgrade setuptools```
1.	In order to use CircuitPython, we need to install a library called adafruit_blinka. We can complete it by running the following script. It may take a while to complete the installation. Please be patient. Choose Y to Reboot Now after the installation:
```  
    sudo pip3 install --upgrade adafruit-python-shell
    wget https://raw.githubusercontent.com/adafruit/Raspberry-Pi-Installer-Scripts/master/raspi-blinka.py
    sudo python3 raspi-blinka.py
```
6.	Install BME280 library using command: 
  ```sudo pip install adafruit-circuitpython-bme280```
7.	Download the example code, connect BME280 to the RPi, and check if it works:
```
   wget https://raw.githubusercontent.com/JZ2211/IIoT_module5/main/demo_bme280.py
   wget https://raw.githubusercontent.com/JZ2211/IIoT_module5/main/savedata_locally.py
   python demo_bme280.py
```  
8.	Check if Flask is installed:  ```pip show flask```
1.	If not, please install flask before continue: ```sudo apt install python3-flask```
1.	Install plotly and pandas (or pip3 if the default is not python3): 
  ```
   pip install plotly 
   pip install pandas
```
11.	If there is an error to import pandas: ```libf77blas.so.3: cannot open shared object file: No such file or directory.``` Please run (See reference at: https://numpy.org/devdocs/user/troubleshooting-importerror.html): 
  ```sudo apt-get install libatlas-base-dev```
1.	Download case1 package from github in the Raspberry Pi (assume to the home directory /home/pi/):
```
   git clone https://github.com/JZ2211/IIoT_Case1.git
```
13.	Please make sure IIoT_Case1 and sub-directories LocalSite and templates has the write permission for the user owner. If not, change the permission using chmod u+w.
1.	Obtain the IP address of the host using ```ifconfig``` or ```hostname -I```, this IP address will be used to access the web server.
1.	Check if the example code program works: 
 ```python IIoT_Case1/bme280_example.py```
1.	Open another ssh terminal, run: 
  ```python IIoT_Case1/LocalSite/localsite.py```
1.	If it works, setup crontab to run in the background. Run:
  ```crontab -e```
Add the following lines to the crontab file:
```
  @reboot sleep 10 && python /home/pi/IIoT_Case1/bme280_example.py
  @reboot sleep 20 && python /home/pi/IIoT_Case1/LocalSite/localsite.py
  0 0 * * 0 sudo reboot
```
18.	Reboot the RPi and now you can access the site use the url: ```http://<ip-address>:5000/<sensorID>``` for the most recent data in plain text display or ```http://<ip-address>:5000/<sensorID>/plots``` for plots. For example, 192.168.1.2:5000/sensor1  or 192.168.1.2:5000/sensor1/plots.


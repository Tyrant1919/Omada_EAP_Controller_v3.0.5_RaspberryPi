login. Should start in /home/pi

sudo apt-get update  
sudo apt-get upgrade  
sudo wget https://static.tp-link.com/2018/201811/20181108/Omada_Controller_V3.0.5_Linux_x64.deb.zip  
unzip Omada_Controller_V3.0.5_Linux_x64.deb.zip  
sudo rm Omada_Controller_V3.0.5_Linux_x64.deb.zip  
sudo dpkg -i Omada_Controller_V3.0.5_Linux_x64.deb  

Confirm install directory. Should complete succesfull-ish. Will ask to install jsvc

sudo apt-get install jsvc  
apt --fix-broken install

Will try to start but fail

sudo nano /opt/tplink/EAPController/bin/control.sh
###
  	Change: JRE_HOME="${OMADA_HOME}/jre"
	To:	JRE_HOME="/usr/lib/jvm/java-8-openjdk-armhf"
	
	Change: JAVA_OPTS="-server -Xms128m -Xmx1024m -XX:MaxHeapFreeRatio=60 -XX:MinHeapFreeRatio=30  -XX:+HeapDumpOnOutOfMemoryError -Deap.home=${OMADA_HOME}"
	To:     JAVA_OPTS="-Xms128m -Xmx1024m -XX:MaxHeapFreeRatio=60 -XX:MinHeapFreeRatio=30  -XX:+HeapDumpOnOutOfMemoryError -Deap.home=${OMADA_HOME}"
	
	Change: ${PORTT_TOOL} 127.0.0.1 ${HTTP_PORT} 500
	To:	netstat -plnt | grep :::8088
###
sudo reboot now
### controller should be running after restart ###

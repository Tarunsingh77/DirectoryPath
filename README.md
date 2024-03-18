
## Email Alert Working Directory Path 

### Heatmap Directory

No-Pedestrian-Zone Heatmap Text Directory
```bash
/media/transpix/hdd1/programs/heatmap/no_ped
```
No-Vest Heatmap Text Directory
```bash
/media/transpix/hdd1/programs/heatmap/no_vest
```
Over-Speeding Heatmap Text Directory
```bash
/media/transpix/hdd1/programs/heatmap/speed
```
### Database
There are four table in database 1. users, 2. detection_data, 3. objectdetection_types and 4. cameras
Please use following command to open the MySQl database
```bash
sudo mysql
```
please enter the ssh login password for get access 
```bash
select * from heatmap.detection_data limit 20;
```
if you want to see all table data then 
```bash
select * from heatmap.detection_data;
select * from heatmap.objectdetection_types;
select * from heatmap.cameras;
select * from heatmap.users;
```
## kafka server
service file running on path for kafka-zookeeper (Zookeeper is a service that Kafka uses to manage its cluster state and configurations)
```
sudo nano /etc/systemd/system/zookeeper.service
sudo nano /etc/systemd/system/kafka.service
```
Status, start and stop Kafka and Zookeeper Service
```
sudo systemctl enable zookeeper
sudo systemctl start zookeeper
sudo systemctl status zookeeper

sudo systemctl enable kafka
sudo systemctl start kafka
sudo systemctl status kafka

```
### Heatmap service
Heatmap alert script uses systemd timers and services
Python script file (located at /media/transpix/hdd1/programs) Speed_heatMap_Alert.py, No_Ped_Alert.py and no_vest_Alert.py
 To see the running status you can use following command
 ```
 sudo systemctl status heatmap.timer
 ```
 To see the timer file 
 ```
 sudo nano /etc/systemd/system/heatmap.timer
 ```
### Email Alert service
Python script file (located at /media/transpix/hdd1/programs) Alerts_Consumer.py
To see the Email Alert service file and status 
```
sudo nano /etc/systemd/system/alert.service
sudo systemctl status alert.service
```
### Dashboard
currently i have not created service file for it but you can run dashboard java compiled file  (located at /media/transpix/hdd1/programs)GXO_Dashboard-0.0.1.jar
```
java -jar GXO_Dashboard-0.0.1.jar --spring.datasource.url=jdbc:mysql://localhost:3306/heatmap --spring.datasource.username=transpix --spring.datasource.password=password --spring.jpa.properties.hibernate.dialect = org.hibernate.dialect.MySQL8Dialect
```








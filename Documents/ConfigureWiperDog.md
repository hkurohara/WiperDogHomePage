We now describe how to configure WiperDog(or this is just a short tour around WiperDog).

Try to control WiperDog
-------------------------------
First you need to enter WiperDog main menu from XWiki's top page

[<img src="http://demo.wiperdog.org/wordpress/wp-content/uploads/2013/09/You-will-see-WiperDog-space-after-installation-completed-232x300.png" alt="You will see WiperDog space after installation completed" width="232" height="300" class="alignnone size-medium wp-image-499" />](http://demo.wiperdog.org/wordpress/wp-content/uploads/2013/09/You-will-see-WiperDog-space-after-installation-completed.png)

You will see  
[<img src="http://demo.wiperdog.org/wordpress/wp-content/uploads/2013/09/WiperDog-main-menu_s-274x300.png" alt="WiperDog main menu_s" width="274" height="300" class="alignnone size-medium wp-image-501" />](/wordpress/wp-content/uploads/2013/09/WiperDog-main-menu_s-274x300.png)

Enter to the menu "Start, Stop... wiperdog server (the same machine)".  
[<img src="http://demo.wiperdog.org/wordpress/wp-content/uploads/2013/09/StartStopWiperdog-300x260.png" alt="StartStopWiperdog" width="300" height="260" class="alignnone size-medium wp-image-502" />](/wordpress/wp-content/uploads/2013/09/StartStopWiperdog-300x260.png)

The red alert saying "Unknown macro: tabs" is harmless, never mind.  
Press "START" button to start WiperDog Server.  
After a second, press "STATUS" button to check the status of WiperDog Server, it may take some seconds, if you don't get 

    "HTTP/1.1 200 OK Content-Type: text/html Content-Length: 0 Server: Jetty(7.6.8.v20121106)"

string, please wait for more few second, then retry to press "STATUS" button.  

If you can't get successfull result, check your WiperDog server configuration described [Download & Install WiperDog](/documents/how-to-install/).

Configure your database connection settings 
--------------------------------------------------
From WiperDog main menu, enter to "Configuration of Database Info" menu.

[<img src="http://demo.wiperdog.org/wordpress/wp-content/uploads/2013/09/DBConfig1-245x300.png" alt="DBConfig1" width="245" height="300" class="alignnone size-medium wp-image-503" />](/wordpress/wp-content/uploads/2013/09/DBConfig1-245x300.png)

This page is for setting up connetion data for database targets you would like to monitor.  
You can modify/create new connection entry by using the panel "Add new data".    

| Item name                       | meaning & usage |
|:-------------------------------:|:------------:|
| Database type                   | type of database you are going to connect to.|
| Host id                         | Symbolic name for the target host, which is not necessally be real host name. |
| Host name                       | IP address or hostname of target database host. |
| Port                            | IP port number of database process, following values are the default port number for each database types.<br/>MySQL: 3306<br/>Postgres: 5432<br/>SQLServer: 1433 |
| Set host ID as a DBinfo element | If this checkbox is on, 'Host id' is prepended to the key of this entry to distinguish with other similar(but for other host) entry. |
| Username                        | User name for database connection.|
| Sid                             | This is only useful for SQL Server monitoring because SQL Server can have multiple instalces on one DBMS insatllation.<br>Set Instance name here.|
| Set Sid as a DBinfo element     | If this checkbock is on, 'Sid' is appended to distinguish other similar(but for another instance) entry. |


If you are monitoring MySQL on the same machine which WiperDog server runnning, you can create setting entry as:

| | |
|:-------------------------------:|:------------:|
|Database type:                   | MySQL        |
|Host id:                         | localhost    |
|Host name:                       | localhost    |
|Port:                            | 3306         |
|Set host ID as a DBinfo element: | off          |
|Username:                        | root         |
|Sid:                             |              |
|Set Sid as a DBinfo element:     | off          |

As other sample, You are going to monitor MySQL server running on the host 'dbhost1', 'dbhost2'.
You need to create 2 entry:  

* entry-A
| | |
|:-------------------------------:|:------------:|
|Database type:                   | MySQL        |
|Host id:                         | dbhost1      |
|Host name:                       | dbhost1      |
|Port:                            | 3306         |
|Set host ID as a DBinfo element: | on           |
|Username:                        | root         |
|Sid:                             |              |
|Set Sid as a DBinfo element:     | off          |

* entry-B
| | |
|:-------------------------------:|:------------:|
|Database type:                   | MySQL        |
|Host id:                         | dbhost2      |
|Host name:                       | dbhost2      |
|Port:                            | 3306         |
|Set host ID as a DBinfo element: | on           |
|Username:                        | root         |
|Sid:                             |              |
|Set Sid as a DBinfo element:     | off          |

After you entered values, you have to press "ADD" button to create(or update) the entry.
And for all configurations take effect, you should press  "CREATE DB INFO" button.


Please keep in mind, DB Connection settings are required to monitoring jobs runnable.

### Set up DB Connection password
As you know, DB Connection requires connection password.  
We store passwords into crypted files.  
To create these files, you need to use 'gendbpassword' command included in WiperDog server package.

Here is sample usage:

     $ bin/gendbpasswd.sh -t @MYSQL -u root
     DBType:@MYSQL
     Username:root
     HostId:null
     Sid:null
     ------------------------------
     
     Password: <---- enter password for root here.
     Update password successfully in password file .dbpasswd_@MYSQL
Above sample creates password data for the DB Info key "@MYSQL".
If you need to create password data for the DB Info key "myserver-@MYSQL", command line will be like: 

     $ bin/gendbpassword.sh -t @MYSQL -h myserver -u root

Created password data are stored into apropriate place and automatically used by WiperDog server.

Configure to make jobs scheduled
--------------------------------------------------
From WiperDog main menu, enter to "Create new Job or Update Job".

[<img src="http://demo.wiperdog.org/wordpress/wp-content/uploads/2013/09/JobConfiguration1-300x293.png" alt="JobConfiguration1" width="300" height="293" class="alignnone size-medium wp-image-513" />](/wordpress/wp-content/uploads/2013/09/JobConfiguration1-300x293.png)

This screen is for creating or modifying WiperDog monitoring jobs.
But in this tour, I use this screen for configuring schedules for 'preset' jobs.

Top part of this screen, you can select "DB Type" from dropdown menu, your choice of "DB Type" create "Jobs" dropdown list.
If you get some errors here, please check WiperDog server configuration described [here](/documents/how-to-install/).

[<img src="http://demo.wiperdog.org/wordpress/wp-content/uploads/2013/09/JobConfiguration3-261x300.png" alt="JobConfiguration3" width="261" height="300" class="alignnone size-medium wp-image-514" />](/wordpress/wp-content/uploads/2013/09/JobConfiguration3-261x300.png)

Select one of jobs you want to try to make scheduled.

Then scroll down to bottom off this screen.

[<img src="http://demo.wiperdog.org/wordpress/wp-content/uploads/2013/09/JobConfiguration4-300x264.png" alt="JobConfiguration4" width="300" height="264" class="alignnone size-medium wp-image-515" />](/wordpress/wp-content/uploads/2013/09/JobConfiguration4-300x264.png)

This part is just for creating scheduled instance of job.
"Instance name" can be any name you like to distinguish from another instance.  
"Schedule" is for schedule string, used to make job instance called continuously(or may be one shot).
I recommend you to set here as "60i", means "this job instance will be called continuously in 60 seconds interval".  

"Params" box is for applying instance parameters.
Remenber the part "Configure your database connection settings" above.
If you are going to connect to the server located on the same host WiperDog runnning, you don't need to set this part.
But if the DB Info key which you are going to connect to contains HostId and/or Sid, you have to set it here like:  

name: dbHostId  
value: _HostId\_of\_DB\_Info\_key_ 

 -> press add button

name: dbSid  
value: _Sid\_of\_DB\_Info\_key_

 -> press add button

After that, you have to press "ADD TO LIST INSTANCE OF JOB", then press "SAVE" button to take above settings take effect.

If your configurations are correct, the job you selected will  be called on the schedule you configured.

The data jobs collected are stored mongodb after that, you can see charts of these data at "MonitoringData" screen(menu name is "WiperDog for view data monitoring")


# Nagios ~ Process Monitoring 


This script allows the possibility to monitor if a process is running or not.

# Configuration

* Install NRPE and dependencies in the Nuxeo Server
* * In Ubuntu you can satisfy these dependencies with the following command: apt-get install openssl nagios-nrpe-server nagios-plugins nagios-plugins-basic nagios-plugins-standard
* Copy the script in /usr/lib/nagios/plugins/
* Edit /etc/nagios3/nrpe.cfg to include your command
* In your Nagios server edit your /etc/nagios3/conf.d/<server>.cfg to add the service for monitoring 

# Example nrpe.cfg 

```
# Nuxeo 6.0 - nuxeo60.domain.com
command[check_nuxeo_process]=sudo /usr/lib/nagios/plugins/check_longrunning_proc --file /home/nuxeo/nuxeo-cap-6.0-tomcat/log/nuxeo.pid
```

# Example my_nuxeo_server.cfg

```
# Nuxeo 6.0 service
define service{
        use                             generic-service
        host_name                       nuxeo60.instance.com
        service_description             Instance of Nuxeo 6.0
        check_command                   check_nrpe_1arg!check_nuxeo_process
}
```


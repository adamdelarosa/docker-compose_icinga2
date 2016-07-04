#icinga2
This repository contains the source for the
icinga2 docker
image.

Image details
Based on debian:jessie
Supervisor, Apache2, MySQL, icinga2, icinga-web, icingacli, icingaweb2, and icingaweb2 director module
No SSH. Use docker exec or nsenter
If no passwords are not supplied, they will be randomly generated and shown via stdout.
Automated build
docker pull jordan/icinga2
Usage
Start a new container and bind to host's port 80

#sudo docker run -p 80:80 -t jordan/icinga2:latest
Start a new container and supply the icinga and icinga_web password

#sudo docker run -e ICINGA_PASSWORD="icinga" -e ICINGA_WEB_PASSWORD="icinga_web" -t jordan/icinga2:latest
The Icinga Web interface is accessible at http://localhost/icinga-web with the credentials root:password

Icinga Web 2
Icinga Web 2 can be accessed at http://localhost/icingaweb2 with the credentials icingaadmin:icinga

Graphite
The graphite writer can be enabled by setting the ICINGA2_FEATURE_GRAPHITE variable to true or 1 and also supplying values for ICINGA2_FEATURE_GRAPHITE_HOST and ICINGA2_FEATURE_GRAPHITE_PORT. This container does not have graphite and the carbon daemons installed so ICINGA2_FEATURE_GRAPHITE_HOST should not be set to localhost.

Example:

#sudo docker run --link graphite:graphite -e ICINGA2_FEATURE_GRAPHITE=true -e ICINGA2_FEATURE_GRAPHITE_HOST=graphite -e ICINGA2_FEATURE_GRAPHITE_PORT=2003 -t jordan/icinga2:latest
Icinga Director
The Icinga Director Icinga Web 2 module is installed and enabled by default. You can disable the automatic kickstart when the container starts by setting the DIRECTOR_KICKSTART variable to false. To customize the kickstart settings, modify the /etc/icingaweb2/modules/director/kickstart.ini



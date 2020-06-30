# check_unix_disk_space
nagios check for free / used disk space on UNIX-like filesystems

This script is executed remotely on a monitored system by the NRPE or check_by_ssh methods available in nagios.

If you are using the check_by_ssh method, you will need a section in the services.cfg
file on the nagios server that looks similar to the following.
This assumes that you already have ssh key pairs configured.
    # Define service for checking free space in filesystem
    # If no thresholds are specified, default to warn=10% critical=5%
    # Thresholds may be defined in %,K,M,G,P (or combinations thereof)
    define service{
            use                             generic-24x7-service
            host_name                       unix11
            service_description             Disk /var/log free space check
            check_command                   check_by_ssh!"/usr/local/nagios/libexec/check_aix_disk_space --warn=10 --critical=5 /var/log"
            }
    

If you are using the check_nrpe method, you will need a section in the services.cfg file on the nagios server that looks similar to the following.
This assumes that you already have ssh key pairs configured.
   define service{
           use                             generic-24x7-service
           host_name                       unix11
           service_description             Disk /var/log free space check
           check_command                   check_nrpe!disk_/var/log -t 30
           }
  


# check_file_exact
# Modify nagios plugin check_file_age to check if the size is exactly something.
#Define this at your Nagios server commands.cfg
define command{
        command_name    check_file_exact
        command_line    $USER2$/check_nrpe -n -H $HOSTADDRESS$ -c check_file_exact -a $ARG1$ $ARG2$
        }

#Add check below
define service{
        use                     generic-service
        host_name               HOSTNAME
        service_description     DESCRIPTION
        check_command           check_file_exact!FILEFULLPATH!SIZEINBYTE
}

#Put check_file_exact at plugins directory
#Add this line to monitoring target's nrpe.cfg
command[check_file_exact]=/usr/lib64/nagios/plugins/check_file_exact -f $ARG1$ -C $ARG2$

 <h2>A. Create a script that uses the following keys:</h2></br>
1. When starting without parameters, it will display a list of possible keys and their description.</br>
2. The --all key displays the IP addresses and symbolic names of all hosts in the current subnet.</br>
3. The --target key displays a list of open system TCP ports.</br>
   The code that performs the functionality of each of the subtasks must be placed in a separate function
  
 ```python
 #!/bin/bash
echo "nmap tool is required to complete this task"
echo "Checking if nmap is installed..."
sleep 1
# Checking if nmap is installed
apt list --installed 2>/dev/null | grep "nmap" > .tmp
if [ -s .tmp ]; then
    echo "nmap is already installed"
    else
        echo "nmap tool is missing"
        echo "Executing nmap installation..."
        sudo apt install nmap -y
        wait
        if [ $? -eq 0 ]; then
            echo "nmap has been installed successfully"
            else
                "Install nmap manually"
        fi
fi 
rm -f .tmp
# First function to scan active hosts on particular subnet
all ()
{
    ipv4patternsub="([0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\/([1-2][0-9]|[3][0-1]))"
    echo "Please enter subnet address and prefix for scan in a format *.*.*.*/* :" ; read net
    if [[ $net =~ $ipv4patternsub ]]; then
        nmap -sn $net
        else
            echo "Enter correct subnet format"
    fi
}
#Second function to scan open ports on particular system
target ()
{
    ipv4pattern="([0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3})"
    echo "Please enter target system IP address" ; read sysip
    if [[ $sysip =~ $ipv4pattern ]]; then
        nmap $sysip
        else 
            echo "Enter correct IP address format"
    fi
}
# Executing functions according to user input
case $1 in
    --all)
        all
    ;;
    --target)
        target
    ;;
    *)
        echo -e "Script usage:\n --all to list active hosts on required subnet\n --target to list open ports on required host"
    ;;
esac 
 ```


<img src="https://github.com/korotetskiy/img/blob/main/bash_a.png">
 
 <head>
    <meta charset="UTF-8">
    <link rel="stylesheet" href="essets/Css/style.css">
</head>
<h2>B. Using Apache log example create a script to answer the following questions:</h2></br>
1. From which ip were the most requests?</br>
2. What is the most requested page?</br>
3. How many requests were there from each ip?</br>
4. What non-existent pages were clients referred to?</br>
5. What time did site get the most requests?</br>
6. What search bots have accessed the site? (UA + IP)</br>

```python
#!/bin/bash
# Checking logfile path
echo "Please enter logfile path"; read logfile
if [ -e $logfile ]; then
    while :
    do
        # Setting up options menu according to the task
        echo "Please choose the option: "
        echo "1. From which ip were the most requests?"
        echo "2. What is the most requested page?"
        echo "3. How many requests were there from each ip?"
        echo "4. What non-existent pages were clients referred to?"
        echo "5. What time did site get the most requests?"
        echo "6. What search bots have accessed the site? (UA + IP)"
        echo "Type [Q] to exit the script"
        echo " "
        printf "Type [1-6] : \n" ; read option
            case $option in
                # 1. From which ip were the most requests?
                1) cat $logfile | awk '{ print $1 }' | uniq -c | sort -nr | head -5
                    printf "\n\n"
                    ;; 
                
                # 2. What is the most requested page?
                2) cat $logfile | awk '{ print $7 }' | uniq -c | sort -nr | head -3
                    printf "\n\n"
                    ;;

                # 3. How many requests were there from each ip?
                3) cat $logfile | awk '{ print $1 }' | uniq -c | sort -nr | awk '{ print $1 " " "requests" " " "from:" " " $2 }'
                    printf "\n\n"
                    ;;
                
                # 4. What non-existent pages were clients referred to?
                4) printf "Non-existent pages referred by clients: %s\n\n"
                    cat $logfile | awk '{ print $9,$7 }' | grep "404" | awk '{ print $2 }' | tee file
                    printf "%s\nTotal: $(cat file | wc -l) files %s\n"
                    printf "\n\n"
                rm -f file
                    ;;
                # 5. What time did site get the most requests?
                5) requests () {
                        printf "between 8:00 and 9:00:\t"
                        cat $logfile | awk '{print $4}' | sed 's/\[//g' | sed -n '/25\/Apr\/2017\:08./ p' | printf "`wc -l` requests\n"
                        printf "between 9:00 and 10:00\t"
                        cat $logfile | awk '{print $4}' | sed 's/\[//g' | sed -n '/25\/Apr\/2017\:09./ p' | printf "`wc -l` requests\n"
                        printf "between 10:00 and 11:00\t"
                        cat $logfile | awk '{print $4}' | sed 's/\[//g' | sed -n '/25\/Apr\/2017\:10./ p' | printf "`wc -l` requests\n"
                        printf "between 11:00 and 12:00\t"
                        cat $logfile | awk '{print $4}' | sed 's/\[//g' | sed -n '/25\/Apr\/2017\:11./ p' | printf "`wc -l` requests\n"
                        printf "between 12:00 and 13:00\t"
                        cat $logfile | awk '{print $4}' | sed 's/\[//g' | sed -n '/25\/Apr\/2017\:12./ p' | printf "`wc -l` requests\n"
                        printf "between 13:00 and 14:00\t"
                        cat $logfile | awk '{print $4}' | sed 's/\[//g' | sed -n '/25\/Apr\/2017\:13./ p' | printf "`wc -l` requests\n"
                    }
                    topreq=$(requests | awk '{print $5}' | sort -nr | sed -n '1 p')
                    requests | sed -n "/$topreq/p" | sed -n 's/^/Site got most requests /p' | sed -n 's/and [0-9][0-9]\:00/&\-/p'
                    printf "\n\n"
                    ;; 
              
                # 6. What search bots have accessed the site?
                6) cat $logfile | awk '/[B|b][O|o][T|t]/{print $1,$12,$13,$14,$15,$16,$17}'  | sed 's/\(\"Mozilla\/5\.0\|(compatible\;\|Linux x86\_64\)//g' | \
                    sed -n '/[B|b][O|o][T|t]/p' | uniq -c | sort -nr
                    printf "\n\n"
                        ;;
                q|Q) break ;;
                *) echo "Please choose [1-6] or type [Q] to exit"
            esac
    done  
else
    echo "Path is not valid. Please enter correct logfile path"
fi
```
<img src="https://github.com/korotetskiy/img/blob/main/bash_b.png">
<head>
    <meta charset="UTF-8">
    <link rel="stylesheet" href="essets/Css/style.css">
</head>
<h2>C. Create a data backup script that takes the following data as parameters:</h2></br>
1. Path to the syncing directory.</br>
2. The path to the directory where the copies of the files will be stored.</br>
In case of adding new or deleting old files, the script must add a corresponding entry to the log file
indicating the time, type of operation and file name. [The command to run the script must be added to
crontab with a run frequency of one minute] </br>    

```python
#!/bin/bash
# Passing source and target directory paths as arguments

if [[ -d $1 ]]; then 
    :
    else
        printf "Specify syncing directory\n"
        exit 2
fi
if [[ -d $2 ]]; then
    :
    else
        printf "Specify target backup directory\n"
        exit 2
fi

# Executing directory sync and specifying log file including entries indicating the time, type of operation and file name
rsync -avtuh --delete --log-file=/var/log/syncdir_logfile --log-file-format="%'i %'f" $1 $2

# See 3_syncdir_logfile to check the script log output
# See 3_crontab file for implementing cron job for this script according to the task
```
<H2>Crontab config</h2>

```python
# /etc/crontab: system-wide crontab
# Unlike any other crontab you don't have to run the `crontab'
# command to install the new version when you edit this file
# and files in /etc/cron.d. These files also have username fields,
# that none of the other crontabs do.

SHELL=/bin/sh
# You can also override PATH, but by default, newer versions inherit it from the environment
#PATH=/usr/local/sbin:/usr/local/bin:/sbin:/bin:/usr/sbin:/usr/bin

# Example of job definition:
# .---------------- minute (0 - 59)
# |  .------------- hour (0 - 23)
# |  |  .---------- day of month (1 - 31)
# |  |  |  .------- month (1 - 12) OR jan,feb,mar,apr ...
# |  |  |  |  .---- day of week (0 - 6) (Sunday=0 or 7) OR sun,mon,tue,wed,thu,fri,sat
# |  |  |  |  |
# *  *  *  *  * user-name command to be executed
17 *	* * *	root    cd / && run-parts --report /etc/cron.hourly
25 6	* * *	root	test -x /usr/sbin/anacron || ( cd / && run-parts --report /etc/cron.daily )
47 6	* * 7	root	test -x /usr/sbin/anacron || ( cd / && run-parts --report /etc/cron.weekly )
52 6	1 * *	root	test -x /usr/sbin/anacron || ( cd / && run-parts --report /etc/cron.monthly )
#
* * * * *   vkor     /home/vkor/skripts/task_C.sh /home/vkor/source_backup/ /tmp/target_backup/ > /dev/null 2>&1
```
    


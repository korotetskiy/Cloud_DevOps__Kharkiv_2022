  <head>
    <meta charset="UTF-8">
    <link rel="stylesheet" href="essets/Css/style.css">
</head>
    <div class="starter-template">
      <h1>Home tasks</h1>
      <head>
    <meta charset="UTF-8">
    <link rel="stylesheet" href="essets/Css/style.css">

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



    
    > cd /etc/ansible/
    > ls -la
    drwxr-xr-x   3 root root  4096 Nov 18 12:22 .
    drwxr-xr-x 122 root root  4096 Nov 10 15:03 ..
    -rw-r--r--   1 root root 20340 Nov 15 13:58 ansible.cfg
    -rw-r--r--   1 root root   615 Nov 18 12:22 hosts



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



    
    > cd /etc/ansible/
    > ls -la
    drwxr-xr-x   3 root root  4096 Nov 18 12:22 .
    drwxr-xr-x 122 root root  4096 Nov 10 15:03 ..
    -rw-r--r--   1 root root 20340 Nov 15 13:58 ansible.cfg
    -rw-r--r--   1 root root   615 Nov 18 12:22 hosts



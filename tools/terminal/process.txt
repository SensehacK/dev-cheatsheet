# Process


Finding process list and other commands



## Kill Process

Find the process ID
> ps -A | grep ringcentral | awk '{print $1}'

Kill the process
> kill -9 32523

Kill the process using name
> pkill -x RingCentral

[SO](https://apple.stackexchange.com/questions/354954/how-can-i-quit-an-app-using-terminal)

[process wildcards](https://osxdaily.com/2012/10/18/kill-process-wildcards-pkill-mac-os-x/)
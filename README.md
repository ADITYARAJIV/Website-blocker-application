# Website-blocker-application
A python application that restricts entry into websites during some part of day.

Libraries used in this application are time and datetime for getting the current time of the day and also to give a delay in responding.
The coding part is very simple.

We first decide a duration in which we want to block the websites. We also decide which websites have to be blocked.
The we check if our current time is in the duration.
If it is then we write to the hosts file local machine ip address and the website(domain) name.
If it is outside the duration then we erase the file contents.

For more in depth understand please watch the video:
https://youtu.be/onHm4Lj5p0Y

Initial this was the code i wrote in the video as well

#Creator Aditya Rajiv
#webiste blocker application 

import time
from datetime import datetime as dt

redirect="127.0.0.1"
websites_list=["www.facebook.com","instagram.com","facebook.com","www.instagram.com"]
hosts_path="C:\Windows\System32\drivers\etc\hosts"

now=dt.now()
current_time=now.strftime("%H:%M:%S")
start_time="10:0:0"
end_time="17:0:0"
print(current_time)
while True:
    if start_time<=current_time and current_time<=end_time:
        print("working hours")
        with open(hosts_path,'r+') as file:
            content=file.read()
            for website in websites_list:
                if website in content:
                    pass
                
                else:
                    file.write(redirect+" "+website+"\n")
                    
    else:
        print("Non work hours")
        with open(hosts_path,'r+') as file:
            content=file.readlines()
            file.seek(0)
            for line in content:
                if not any(website in line for website in websites_list):
                    file.write(line)
            file.truncate()
            
    time.sleep(10)

Later change made was that i decided to just truncate the file if it is not needed to be used.
    
    

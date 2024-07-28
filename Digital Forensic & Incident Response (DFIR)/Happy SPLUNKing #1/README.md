![image](https://github.com/user-attachments/assets/3b5bb23c-6c3c-4c00-b5d8-914d04eac062)

Download the file and extract it.

![image](https://github.com/user-attachments/assets/90dec473-8a5b-4423-aae2-7bbd3c1f4818)

![image](https://github.com/user-attachments/assets/3377ea66-74e9-4a3a-aa1b-7add03063e83)

Looks like we got .vmdk file here which could be run using vmware workstation.

![image](https://github.com/user-attachments/assets/246dfd10-53b5-46c0-b257-aef73b3a30fe)

So I booted it up with the provided credentials `ihack24:root` and instantly locate to its log file for auth.log which was located at `/var/log`'s directory.

![image](https://github.com/user-attachments/assets/eef493c0-b5e8-46d4-9b7d-6b55c336c101)

And then I realised, this is too hard to read the logs here. So, I opt for reading it at its splunk server. But the problem is, I don't know how to get the splunk server's URL. Then I check for connection for this machine by using `ping`.

![image](https://github.com/user-attachments/assets/316ac056-048d-4045-aab5-c849391a559a)

I see, lets check the network configuration to see if it could access the network or not.

(PS: From this point, I forgot already how I resolve this so that my ipv4 would appear when I use command like `ip addr show` or `ifconfig`

On the splunk's server, the first thing that I filtered was `index=security EventCode="4625"| reverse` and check the time for when the bruteforce happened. Then I compared it with successful login using this filtered `index=security EventCode="4624"| reverse` and managed to make deduction where if there were any successful login from 9.55PM onwwards, that would be the attacker. But my query for EventCode="4624" was not proven due to its only show log before 9:55PM. So I have to read from another log which is sysmon using `index=sysmon EventCode="4624" | reverse`. 

Then, based on that I make deductions if the attackers were bruteforcing our machine and the target was RDP's service, it would be likely using RDP's port which is 3389. So I filtered the port and check the ip address that involve and I make my assumption that the ip with the most attempts was the targeted machine.

![splnuk3](https://github.com/user-attachments/assets/67db6d3f-6750-47e7-a411-edba8f9a0b21)

![splunk1](https://github.com/user-attachments/assets/643391d2-c9d1-4b45-8046-69826861dce3)

While for the username part, I make deduction based on the account's name being succesful logon from this query `index=security EventCode="4625"| reverse`.

So the flag will be ihack24{admin:192.168.8.52}

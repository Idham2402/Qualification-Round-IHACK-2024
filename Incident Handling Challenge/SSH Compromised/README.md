![image](https://github.com/user-attachments/assets/251d8ae5-1389-482c-87a1-8a3b7da965f6)

Lets download the file and extract it.

![image](https://github.com/user-attachments/assets/8404c98e-d4d4-4d38-b2e3-c9262e259d0b)

![image](https://github.com/user-attachments/assets/e91c3497-afe5-4f05-b7bf-d87b63805a5c)

Looks like we got `auth.log` here which is security log for SSH's session establishment

![image](https://github.com/user-attachments/assets/5fa2fb78-af7b-4ed5-b2fe-4822acbcda67)

So our clue here is "successful login". All I need to do is find the keywords for successful's ssh such as `Success` or `Accepted`.

![image](https://github.com/user-attachments/assets/acfc9b1d-c3a3-4a11-b8c0-7b76e021b4e2)

And... we found it. So the flag will be `ihack24{149.102.244.68_sysadmin}`

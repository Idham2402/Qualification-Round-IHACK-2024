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



![image](https://github.com/user-attachments/assets/6a640253-281b-41de-a1ee-1c432520f652)

Lets visit the url

![image](https://github.com/user-attachments/assets/2df344bf-3b51-406e-9dd9-0fda0e552279)

Lets check for its source code and anything using browser's extension like Wappalyzer.

![image](https://github.com/user-attachments/assets/670716ba-7e43-48b2-8374-b2af7d120931)

Found nothing strange/exploitable yet... Lets register whatever account first and login with that credentials

![image](https://github.com/user-attachments/assets/63a03c7e-4ed4-4e4e-a6b0-b482ecaa9b83)

Ok looks like we managed to create an account and login with it

![image](https://github.com/user-attachments/assets/f2b8152c-1c00-4fd5-8c64-cb5ebe3d2ad6)

Inspect the source code for our Home's page, My account, Support and Feedback to see if anything useful could be found. 

Home's page doesn't reveal anything, Support's page reveal the admin's email.. Ok that's very useful for us later on

![image](https://github.com/user-attachments/assets/5cc6b78c-a0d7-42ec-aaaa-e2e6873b9665)

While the Feedback's page have comment's section so I tried to do some xss to inject into the html but nothing happened.

![image](https://github.com/user-attachments/assets/cfef8fb7-1b30-457c-bd73-8157fbc1f87b)

Found something that's exploitable on My account's page.

![image](https://github.com/user-attachments/assets/ca692f1d-e6ce-41ec-9d2c-d52d0d8f20cb)

Noticed that the url show us the userID's value thats not using GUID? Lets try to change it to whatever value to see if we could exploit IDOR for this question. Lets change from 68 to 1.

![image](https://github.com/user-attachments/assets/8d96aeaa-bff8-44c6-8212-4f920991c660)

Yep! It works! So, all I need to do now is enumerate until I found admin's credential. Lets fire up Burp and send it to Intruder.

As usual, add the "§" symbol at our payload and set the payload settings to use numbers. In this case, I chose from 0 to 100 for early testing.

![image](https://github.com/user-attachments/assets/54e09a14-8963-474f-98be-6682b9c257cc)


![image](https://github.com/user-attachments/assets/80c1e765-5881-4046-b969-c58adcfe3667)

Don't forget to add grep so that later on we will be notified if we managed to grep admin's page.

![image](https://github.com/user-attachments/assets/dc6dd896-6c0d-41b6-9f7f-8e2c95386975)

And... we hit the jackpot.

![image](https://github.com/user-attachments/assets/b6771496-d63f-43d0-9ab9-cf08afa4605e)

The admin's page is on userID=53 and there is our flag.

![character journey](https://github.com/user-attachments/assets/d4f0c5d8-fe93-484e-b700-61700fad3cc3)

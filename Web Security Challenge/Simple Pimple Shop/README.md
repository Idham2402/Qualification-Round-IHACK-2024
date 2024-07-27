![image](https://github.com/user-attachments/assets/3dc52817-4498-41b5-9183-6c08e349afc5)

First things first, lets visit the url.

![image](https://github.com/user-attachments/assets/d1c7af66-3771-49e4-aa51-10edd4e41f8f)

Inspected its source code and using browser's extension such as Wappalyzer.

![image](https://github.com/user-attachments/assets/3bce6032-6a0b-43fe-ba83-5f8b16319fed)

Ok... it says that its using Ruby which could be vulnerable for SSTI but lets check other things first.

![image](https://github.com/user-attachments/assets/77187541-914e-46ca-85ca-9ae8d8f18b05)

Hmmm, it has url for the image so lets try for path traversal and see if we manage to get something or not.

![image](https://github.com/user-attachments/assets/1d8a2de9-aefa-4776-9637-4a72d46a00a4)

![image](https://github.com/user-attachments/assets/e7ee46ed-c699-4472-8384-f9b2248ea8be)

And.. hit it enter.

![image](https://github.com/user-attachments/assets/b95720b2-4281-4a05-bd1f-64dfc93d7fff)

Alright looks like path traversal is not our answer. Lets try something else.

Upon further inspection on each cat's page, there is a comment's section available for us.

![image](https://github.com/user-attachments/assets/4d338fc6-3a51-49e5-afc7-d7a89c2435e6)

Comment's section could be vulnerable for xss. Lets test it.

![image](https://github.com/user-attachments/assets/d78cb24a-fd71-45ae-a598-96b0c31ff0ae)

Nice! It works! Lets inject it further with `<script>alert(1)</script>`

![image](https://github.com/user-attachments/assets/cdbb3de6-19b5-4660-9638-749cce108980)








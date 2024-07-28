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

Ok so far so good. Lets try to fetch for our flag. But in this case, we doesn't have any clues about the flag's file name except its format. So i just randomly injected anything that I could think of using payloads from google but still got no results.

After hours of injection and failed. I decided that maybe xss was not the answer for this question. Then I remembered about the page using Ruby as it template.

![image](https://github.com/user-attachments/assets/3bce6032-6a0b-43fe-ba83-5f8b16319fed)

So, without further a do, lets try to inject any Ruby SSTI's payload.

![image](https://github.com/user-attachments/assets/1fdddba6-c030-498e-bebd-d3ff06948245)

Looks like ERB Ruby is not the answer as our expression was not being treated as execution but strings instead. I tried multiple payload such `<%=foobar%>` in hope that it would trigger error but to no avail. (Don't forget to encode our payload first before using it to avoid being sanitized/filtered)

![image](https://github.com/user-attachments/assets/7e1530a8-1071-4c5c-9d56-4876ac2442ab)

Then I tried to put `%0A` in front of my payload and at the end of my payload which act as input bypass validation for ERB Ruby by making our payload appear on the new line and suddenly managed to trigger error.

![image](https://github.com/user-attachments/assets/d196bb14-1957-4fe8-9fc0-ff396ba42dc0)

![image](https://github.com/user-attachments/assets/c1c65cbf-1487-48e0-9608-3be88b5ba04f)

Alright! Looks like we know exactly which Ruby that its using which is Slim(Ruby). So now lets find our Slim SSTI's payload.

![image](https://github.com/user-attachments/assets/98c7cd45-d7bb-4050-8e83-776ff50151d4)

Injected it but it just reflect normally without doing the expression. I was unsatisfied, so I look more into other payloads such as at PayloadsAllTheThings, https://github.com/swisskyrepo/PayloadsAllTheThings/tree/master/Server%20Side%20Template%20Injection#ruby

![image](https://github.com/user-attachments/assets/80aca9fa-e661-401b-9f41-ea446cc65587)

So I tried to use `#{7*7}` instead and boom!

![image](https://github.com/user-attachments/assets/e669d5bf-d6d1-40c3-95e1-15a3a3691803)

Then, I guessed maybe the `#` was something that could bypass input validation. So I googled and ask chatgpt for it and got my answer.

![image](https://github.com/user-attachments/assets/17112f33-d6db-4e4b-8b94-664c45fb7392)

Next, lets find the flag using arbitary command like this `#{ %x|ls| }`

![image](https://github.com/user-attachments/assets/aa7186c1-8019-4cad-82a5-2d26e16b7c1e)

Nice! Lets `#{ %x|cat flag.txt| }` it.

![image](https://github.com/user-attachments/assets/9fb159d9-2e2f-447b-8753-7d7a870931f2)

GG




















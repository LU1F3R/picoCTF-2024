## Problem:

Can you abuse the banner?The server has been leaking some crucial information on

```
tethys.picoctf.net 52584
```

Use the leaked information to get to the server.To connect to the running application use

```
nc tethys.picoctf.net 59321
```

From the above information abuse the machine and find the flag in the /root directory.

## Basic Idea of the Problem:

So when i was solving this challenge, it was kind of a new one for me but it was pretty interesting. So basically you have got two servers, the first one leaks some data through which u need to access the second server and find the flag. 

## Solution:

So first thing first, i logged into the first server, 

![image](https://github.com/LU1F3R/picoCTF-2024/assets/45719646/46cbdde8-b252-41b2-95c9-ac23340446dc)

well nothing here accept of a password which is what we needed for accessing the second server

![image](https://github.com/LU1F3R/picoCTF-2024/assets/45719646/78add35c-2a38-43e2-bb55-b5808c7a14b8)

So after entering the password, and answering some questions that could be searched on google, you enter a shell. Now from here things start getting tricky. First thing everyone CTF player does, check what’s in the directory

![image](https://github.com/LU1F3R/picoCTF-2024/assets/45719646/e6da8ade-5200-4424-bdf1-1dbb5098b2b2)

So you got some kind of banner and some text

When you read both of them, you will see text says '*keep diggin’* and the banner is the one that is displayed in the start. Okay so nothing here. So i tried to go to the parent directories and see what is in there. So after some ‘*diggin’*(pun intended), i reached the root directory in which we saw two files, *flag.txt* and *script.py.*

![image](https://github.com/LU1F3R/picoCTF-2024/assets/45719646/b4c71faa-b483-428f-8118-40c56eac93ae)

Well, i was happy that we found our flag, but it wasnt that easy, cause you are not allowed to read the flag file. When you run the *‘script.py’,* you realise that its the same programme that runs when you connect to the server. And the banner is the same one that we saw in the *player* directory. Well thats interesting given that in the hints, there was mention of symlinks. So now here comes the brainstorming part. 

What if we go to the *player* directory and delete the original banner, then create a symlink of this flag named as banner in the *player* directory so that when we connect to the server, rather than of reading the actual banner, it reads the flag. 

Well this all seemed far-fetched, but it was worth a try. So thats exactly what i did here.

![image](https://github.com/LU1F3R/picoCTF-2024/assets/45719646/e4a7f6a7-9a1f-4e23-970a-58258b6de7b9)

Great so we have our own banner now, which is actually a symlink to *flag.txt*, So all we have to do now is to connect to the server again and hope that it will work.

![image](https://github.com/LU1F3R/picoCTF-2024/assets/45719646/948231fd-fe02-4867-a4f6-51ac23590ccb)

And BINGOO!!!! It worked. Well to be honest, when i first though of this, i had 0 hopes that it will work, but am glad it did. 

A very innovative challenge of using symlinks in a creative way, if they wouldn’t have mentioned symlinks in the hints, trust me, i never would have thought of using them. 

## Flag:

picoCTF{b4nn3r_gr4bb1n9_su((3sfu11y_b3ee718e}

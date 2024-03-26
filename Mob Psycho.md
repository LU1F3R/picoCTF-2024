# Mob Psycho

## Problem:

Can you handle APKs?Download the android apk [here](https://artifacts.picoctf.net/c_titan/52/mobpsycho.apk).

## Basic Idea of the Problem:

Well, loved the name of the challenge tbh…full on anime vibes but whatever. The challenge basically gives you an apk file and then simply expects you to find the flag. It can be anywhere in the apk file. 

## Solution:

Well it was due to the hint tbh, that I thought of unzipping this file. Now there are many tools available online for unzipping an apk file, but i prefer to go for the basics. I simply changed the extension of the file from .apk to .zip and then just unzipped it. So that part was simple. The difficult part was where to look for. You can go for `grep -r`  and something like that for the flag but it wont work. Now generally in CTFs there is a file named *flag* that contains the flag right? So i tried my luck a bit and used `find . -name "flag*"` in the mobpsycho folder to see if there were any files or folders with the name *flag*  in this whole folder. Then after I found a match, i tried. to read it using `cat` and this is what i got

![image](https://github.com/LU1F3R/picoCTF-2024/assets/45719646/bb36ad67-cfb7-4141-a8ae-cac5f575d1a4)

So it seemed like our flag has been converted to hex. So i went to cyberchef and decoded it.

![image](https://github.com/LU1F3R/picoCTF-2024/assets/45719646/9f1e5217-0e00-4279-81df-cd7bd13cff58)

And BINGOO!!! We got out flag. Pretty simple challenge but yeah, thinking of the command could take some time.

## Flag:

picoCTF{ax8mC0RU6ve_NX85l4ax8mCl_85dbd215}

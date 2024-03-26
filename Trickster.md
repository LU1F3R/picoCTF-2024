# Trickster

## Problem:

I found a web app that can help process images: PNG images only!Try it [here](http://atlas.picoctf.net:57185/)!

## Basic Idea of the Problem:

So, a very interesting but kind of obvious problem. You got a website where you are asked to upload png files. It doesn’t accept any but the PNG files. And after it uploads the png. It does nothing. Well basically, it was pretty obvious that it was a file upload vulnerability challenge.

## Solution:

So, first thing first, we needed to know what kind of check were done on the file we upload, so that it believes that well its a PNG file. So I did what every desperate Web Exploit challenge solver do, and hoped there was a robots.txt, and i was lucky because there was.

![image](https://github.com/LU1F3R/picoCTF-2024/assets/45719646/49a390de-8b1c-41dc-aa21-9c316392aa89)

so i tried to see the instructions.txt

![image](https://github.com/LU1F3R/picoCTF-2024/assets/45719646/c4972db1-3c87-4432-9b1e-18d4778ff62f)

Okay so we got the conditions we were looking for:

1. Our file should have the extension .png
2. It should have PNG file’s magic bytes.

Also when i tried to access the uploads folder, we didn’t have the permission. Fishhyy….maybe we need to access that.

Okay so now i first created an empty file called empty.png and then opened the proxy with Burp Suite and intercepted the request of uploading my empty.png on it.

In the request, i updated the name of the file to ‘payload.png.php’ and then wrote some HTML and PHP in it.

![image](https://github.com/LU1F3R/picoCTF-2024/assets/45719646/b3127c05-3566-4ef8-8d4d-034a8941cc25)

Something like this. Basically what this will do will create a form for me, and will execute shell commands on the server.

Now lets access our payload by typing it in the URL and lets add some command in the URL as well for it to execute.

![image](https://github.com/LU1F3R/picoCTF-2024/assets/45719646/7b0c7645-9ffa-464f-b388-8938d3293bfe)

And lessgooo, we can see the files. Lets read the weird named txt. file.

![image](https://github.com/LU1F3R/picoCTF-2024/assets/45719646/b93f8c59-3924-416a-b708-b87f8c04cffd)

BINGOOO!!!! I guess we found the flag.

## Flag:

`picoCTF{c3rt!fi3d_Xp3rt_tr1ckst3r_d3ac625b}`

# IntroToBurp

## Problem:

Try [here](http://titan.picoctf.net:52211/) to find the flag

## Basic Idea of the Problem:

Okay so basically, not very helpful description of the problem sadly. When you visit the link you will see a form. After you fill the form, you are asked for the otp, which is basically something you don’t know. Our challenge is to try to overcome that OTP thing.

## Solution:

Well, since the name suggest, we had to use Burp Suite. I opened the proxy, tried to intercept the requests, but couldn’t get much idea. Tried to change the requests. Thought of many possible attacks. CSRF token was there in this challenge, so client-side-request-forgery was protected. After spending hours, I had this silly idea of completely removing the OTP parameter from the request. Like when you intercept the request for the authentication you see something like this:

![image](https://github.com/LU1F3R/picoCTF-2024/assets/45719646/f4f296a3-b2cb-4a1c-a70e-7b2243b7a23c)

So if we just remove the otp parameter before forwarding the request then?

Well then the site just keep loading. It didn’t work. But then i realised, maybe it required some parameter, not necessarily ‘otp’. So instead of the ‘OTP’ parameter, i renamed it with something like, ‘var’

![image](https://github.com/LU1F3R/picoCTF-2024/assets/45719646/01946527-9d39-48af-b504-7e84f8273796)

And when i forward this request….

![image](https://github.com/LU1F3R/picoCTF-2024/assets/45719646/a8c56b45-d87a-438c-a72c-56775de0c844)

BINGOO1!!! We have the flag. Pretty stupid, but it was what it was ; )

## Flag:

picoCTF{#0TP_Bypvss_SuCc3$S_e1eb16ed}

# Blast from Past

## Problem:

The judge for these pictures is a real fan of antiques. Can you age this photo to the specifications?Set the timestamps on this picture to 1970:01:01 00:00:00.001+00:00 with as much precision as possible for each timestamp. In this example, +00:00 is a timezone adjustment. Any timezone is acceptable as long as the time is equivalent. As an example, this timestamp is acceptable as well: 1969:12:31 19:00:00.001-05:00. For timestamps without a timezone adjustment, put them in GMT time (+00:00). The checker program provides the timestamp needed for each.Use this [picture](https://artifacts.picoctf.net/c_mimas/74/original.jpg). Submit your modified picture here: nc -w 2 mimas.picoctf.net 54246 < original_modified.jpg

Check your modified picture here: nc -d mimas.picoctf.net 52368 

## Basic Idea of Problem:

So you have been given an image and you are asked to edit its time stamp so that when analysed this photo seems to be of 1970.

Well technically the approach is quite simple, either u guys can use some tools for this or you can follow my method for editing through the hex editor.

## Solution:

First we will analyse the image and see its metadata using exiftool.

![image](https://github.com/LU1F3R/picoCTF-2024/assets/45719646/ad7ae2bc-37ad-4a2e-8730-113198cf7c77)


![image](https://github.com/LU1F3R/picoCTF-2024/assets/45719646/9e988f9c-77d3-44cb-a41b-847e7e860980)

So we can see that currently the dates are set to 2023:11:20. Now we need to edit this metadata so that we can set the dates to the required date.

If you will open this image in a hex editor(i am using Hex Fiend), then u will see something like this:

![image](https://github.com/LU1F3R/picoCTF-2024/assets/45719646/3e43ab27-fa61-47eb-97eb-ea362ac7879f)

On the right side you can see some readable text and if you focus on it you will see some dates. Bingo they are the dates we saw in the metadata of the image. Now you can directly edit the dates to your required date and submit the image.

![image](https://github.com/LU1F3R/picoCTF-2024/assets/45719646/a42a33b2-82f1-4448-a697-be8afeb307f8)

Rename the edited image and submit it the server. Now connect to the server to seee if you passed the checks or not.

![image](https://github.com/LU1F3R/picoCTF-2024/assets/45719646/d18b780f-120e-4982-a220-4f9d9bacfc67)

Well we failed the 4th tag, maybe it wasn’t that easy? Its saying that our meta data have .703 but they need .001. Well if you revisit the hex data of our modified image. You can see some 703 in the text. Edit those to 001.

![image](https://github.com/LU1F3R/picoCTF-2024/assets/45719646/0c51f159-36a0-4d71-89e4-e9d10ef1aa5f)

Now submit the image again to the server and check the results.

![image](https://github.com/LU1F3R/picoCTF-2024/assets/45719646/5ac2838f-fc7c-484f-83d1-01191fce1c8d)

![image](https://github.com/LU1F3R/picoCTF-2024/assets/45719646/da585707-3e33-4716-bcc3-b2bb10dc65ac)

Okay so we have cleared 6 tags, only the 7th one is left. Its saying that the Samsung Timestamp hasn’t been changed. Now this tag took me some time to pass. But if you will go to the end of the hex editor you will find something weird.

![image](https://github.com/LU1F3R/picoCTF-2024/assets/45719646/6024bfd0-427d-4489-b049-0bc30cdf4ed4)

You will see something like Image_UTC_date and some numbers. Those numbers are actually EPOCH number. When you will read about EPOCH number on google, you will find that EPOCH time is basically the amount of seconds passed from the 1970:01:01 00:00:00, which coincidently is out given time.

![image](https://github.com/LU1F3R/picoCTF-2024/assets/45719646/3930740d-89f7-45f7-a99e-88817d9aad1b)

Edit the time to 0000000000001 and now submit the image again.

![image](https://github.com/LU1F3R/picoCTF-2024/assets/45719646/7b943393-543f-4956-a058-d6a36cea112e)

And BINGO!!!!, you have passed the last tag and won the flag…

## Flag:

picoCTF{71m3_7r4v311ng_p1c7ur3_b5f7bcb5}

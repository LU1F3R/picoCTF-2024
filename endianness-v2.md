# **endianness-v2**

## Problem:

Here's a file that was recovered from a 32-bits system that organized the bytes a weird way. We're not even sure what type of file it is.Download it [here](https://artifacts.picoctf.net/c_titan/36/challengefile) and see what you can get out of it

## Basic Idea of the problem:

So in this problem you are given a file, and when u see the file, there is nothing in it. But the problem description give us some idea that we have to edit the Hex data of this file to make it something readable or viewable.

## Solution:

So first step, check the file type:

![image](https://github.com/LU1F3R/picoCTF-2024/assets/45719646/dbf17b65-bf56-40da-98a8-0b1e60cb0cbd)

so nothing much just data. So now I opened it on the hex editor and had a look at its data. Well it was weird and for some time i didnt have any idea. But the problem is named ‘endianness-v2’ so it has something to do with endianness order right? 

So on this thinking, i took the first few bytes of the file and tried to see there different endianness on this site https://www.scadacore.com/tools/programming-calculators/online-hex-converter/

and this is what i got:

![image](https://github.com/LU1F3R/picoCTF-2024/assets/45719646/ec25d336-7f82-4a44-bbd2-e387e9ae8a0a)

Now when i saw the results, something felt familiar. Little Endian form represented some magic numbers i suppose. So i checked for the magic numbers of different file types.

![image](https://github.com/LU1F3R/picoCTF-2024/assets/45719646/6d1b5874-0a66-4d1a-8864-8ad623e112b3)

And damnnn, i was right. These were the magic numbers of JPEG file.

So to solve this challenge what i had to do was:

> Take every 4 bytes of the file, arrange them in little-endian form
> 

So best way to do this was to write a python code. 

```python
def hex_to_little_endian(hex_string):
    little_endian_hex = bytearray.fromhex(hex_string)[::-1]
    return little_endian_hex.hex()

def convert_chunks_to_little_endian(hex_data, chunk_size=8):
    hex_data = hex_data.replace(" ", "")
    chunks = [hex_data[i : i + chunk_size] for i in range(0, len(hex_data), chunk_size)]
    little_endian_chunks = [hex_to_little_endian(chunk) for chunk in chunks]
    return " ".join(little_endian_chunks)

input_hex_data = ""
little_endian_result = convert_chunks_to_little_endian(input_hex_data, chunk_size=8)
print("Little-endian form:", little_endian_result.upper())

```

So put the hex data of the file in the ‘input_hex_data’ variable and you will get the little endian form as output. The catch in this script is to put the data as a multiple of 4 bytes. So if you will copy all data and put, then it will show error ‘cause the file has ‘4k+3’ bytes. So the last 3 bytes can be arranged manually.

![image](https://github.com/LU1F3R/picoCTF-2024/assets/45719646/c88bf24b-e509-4c67-90a3-cdddcc121119)

Now replace the old hex data of the file with the new data:

![image](https://github.com/LU1F3R/picoCTF-2024/assets/45719646/d1883b0f-c105-48e5-8dba-bf9c3b6290a5)

Add the extension ‘.jpeg’ in the file

![image](https://github.com/LU1F3R/picoCTF-2024/assets/45719646/a35b03e7-cb28-47c4-ae47-5bfe831b4150)

And you got the flag!!!!

## Flag:

picoCTF{cert!f1Ed_iNd!4n_s0rrY_3nDian_b039bc14}

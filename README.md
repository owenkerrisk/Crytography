# TLS Cipher Suites

In this project, I will be showing how I was able to apply my cryptography skills with the labs provided.

## Table of Contents

- [Introduction](#Introductuon)
- [Lab1](#lab1)  
- [Lab2](#lab2)  
- [Lab3](#lab3)  
- [Lab4](#lab4)  
- [Conclusion](#conclusion)


### Introduction

Cryptography is a method of encrypting or transforming data into an unreadable format known as cipher text. Cryptography's urgent objective is to discover innovative techniques for producing cryptographic keys at all times. Cryptographers are continually refining and exploring for new ways for generating cryptographic keys in order to successfully accomplish this assignment. This report will focus on labs 1- 4 and I will be focusing on Secret Key Encryption, Pseudo Random Number Generation, MD5 Collision Attack and RSA Public Key Encryption & Signature throughout this report. All these labs were completed on Oracle Box Virtual Machines which will demonstrating all my work I completed throughout this assignment.

![image = 250x250](https://github.com/user-attachments/assets/167812b3-931e-47f6-9157-4283a6736bfa) 

---

### Lab 1
In this lab, the task is to decipher the given cipher text. The scheme used to encipher the text is substitution cipher, which substitute a different letter for each occurrence of the letter. It can be deciphered if a person knows the cipher key. However, a person can easily find the key using frequency analysis, which works on the fact that some of the letters are used more frequently in comparison to others especially in the English language. 

Description:

Task: First the text is viewed in the terminal using cat command and by using the frequency analysis tool provided in the lab document. 

Ans: As a result, the most appeared letter is ‘t’. Which can represent the letter ‘e’, as it’s the most common letter in English language. Then using the trigram analysis of the text, it is found that ‘ect’ and ‘iem’ are the most common words in the given cipher. But we know that ‘t’ represent ‘e’ then ‘ect’ will be the word ‘the’. Additionally, the next most common word is ‘obs’, which represent ‘and’ when deciphered. Using this way allows for some of the words to be completed with missing characters and can be easily completed by guessing the remaining part. 

The screenshot below shows the frequency analysis of single letters, from the cipher text:

![Screenshot 2025-04-03 at 11 02 09](https://github.com/user-attachments/assets/1de6691e-db83-4f03-b551-0588143c382b)

Additionally, the next screenshot shows the trigram analysis of the text:

![Screenshot 2025-04-03 at 11 02 18](https://github.com/user-attachments/assets/a1b2880a-be00-4b3f-82f6-a0801471d9f7)

By using the ‘tr’ command, the letters can be replaced by the actual letters, as shown in the screenshot:

![Screenshot 2025-04-03 at 11 05 39](https://github.com/user-attachments/assets/e3322d48-0941-4287-97db-26699fef9779)



Different Encryption Modes:
AES-128-CBC:

The file plain.txt is encrypted using the KEY and IV, as shown in the screenshot:

 

-BF-CBC:
The file plain.txt is encrypted using a salt, password prompt also appears on the terminal during encryption:

 

AES-256-CBC:

 

In this task the pic_original.bmp is encrypted using ECB and CBC encryption. The below screenshot shows the output of the encryption using ECB:

 

 
After this, the original header of the pic_original.bmp is replaced by the bogus header of the encrypted file. Below screenshot shows the process:

 

Now the encrypted file can be viewed by any image viewer. As shown in the screenshot:

 

As a result, it can identify that the image is still understandable, even after encryption. Next, we will use CBC encryption for the same image.
 
Which we will then view the encrypted image, which is new_cbc.bmp:

 

From this image, the data is completely masked, and we cannot tell anything about the image. So, CBC encryption is preferred over ECB encryption, which still leaks some information of the image.













Lab 2

Random numbers are always required for local key generation and using the best possible ways to get these keys is very important because the information cannot be made as secure as it needs to be. In this lab we will learn wrong way of generating a key and find the problems that can cause problems, as well as the best practices for generating a more secure random key generation.

Description:

The code is copied to the VM and saved as task1.c 
It will then be compiled using GCC compiler and executed three times. As shown:
  

The output of the program shows the time function and its output with the srand() function. Which means that the output changes with the change in time. Different output for different time values. However, if a person knows the key generation time, he will be able to find the key, which makes the whole process to be cracked easily. 
Next the srand () function is commented out and the program is compiled and executed again, as shown:

  

This time the srand() function is not contributing its part in the output, which shows same output each time the program is executed. So, the srand() function is useful in making the output more random in case using it as a key for encryption.


2.3 Task 3:

The following command is used to watch the output of /proc/sys/kernel/random/entropy_avail continuously on the terminal, as shown:

 

After observing different operations to test the entropy, it is observed that opening large files and browsing webpages, increases the entropy. While mouse movement has a significant role in increasing the available entropy, because it uses physical world data.




2.4 Task 4:

In this task the random pool is being observed in real-time, which resides at the location /dev/random, and the output is displayed on the terminal after converting it into hex dump:

 

When all the data is displayed on the terminal the pool gets empty and is blocked, then by moving mouse and clicking on the screen increases the randomness. When the value reaches 63, the command displays another value on the screen by using the randomness from the pool. A hex dump displays 64 bytes of data, so as the decrease in the pool value.








Lab 3

In this lab our task is to create two files with some prefix text, similarly to both files, is to test that whether md5 is collision-resistive or not. 

Description:

To demonstrate the attack, we will use the tool md5collgen. This tool requires a prefix file to create two output files, as shown:

 

If we investigate the hashes of the files, these are the same for different files:

 

By opening each file using the hex editor ‘bless’, we can observe the binary data, as shown:
 

Both the files contain the same prefix in the beginning of the file while some random data is present in the remaining part of the files, which makes the two files different. Furthermore, the hash must be different but still the hash of the files are same, which opposes the collision-resistance property and makes the hash vulnerable to attacks.

Conclusion:

This lab proves that md5 hashes are not collision-resistive and allows attackers to use this vulnerability to crack md5 hashes very easily.










Lab 4

The purpose of this lab is to demonstrate the use of RSA public key encryption and its usefulness in checking the authenticity of a message. It also demonstrates the results when a signature is corrupted or changed by someone.

Description:
In this lab we will focus on the following tasks:
•	Derive the private key
•	Encrypting a message
•	Decrypting a message
•	Signing a message
•	Verifying a signature

Task 1: Derive the private key

	To derive the private key, we will use the program RSATask1.c, which takes the hexadecimal values of p and q and calculates the private key. The program is first compiled using:
		gcc -o Task1 RSATask1.c -lcrypto
After running the program, following private key is generated, as shown:

 

Task 2: Encrypting a Message

The next step is to use the private key to encrypt the message. But the program needs hex code of the message, so the following python command is used to get it:

 

Now, this code will be replaced in the program RSATask2.c and recompiled, to get the encrypted message. The encrypted message is as shown:

 
Task 3: Decrypting a Message

In this task we will decrypt the message, that was encrypted in the last task. For this we will replace the encrypted message in the file RSATask3.c and compile it. The following screenshot shows the replaced characters:

 

Next, I execute the file Task3, and the decrypted message will be displayed as shown:

 

By converting the hex code to plain-text, we can view the actual message, as shown:

 
Task 4: Signing a message

In this task we will generate a signature for the message, highlighted in the program RSATask4.c, as shown:
 
The program is compiled and executed in the terminal to get the signature, as shown:
 

Next, we changed the message hex, such that to observe the effect on the signature. The last two characters of the hex code are changed from 21 to 2F, compiled the program, and executed again. Below screenshot shows the output signature of both the messages:
 

It shows that the signature changes with the change in message and thus keeps the integrity of the message.
Task 5: Verifying a signature

Now, the message is received by Bob, with the signature of Alice. To confirm that the message is from Alice, Bob will use Alice’s public key and check its authenticity. Open the program file RSATask5.c and add the above signature in place of S, as shown:
 
 
Now compile and run then program to get the message in HEX:

 

Then decode the hex to get the original plain text message:

 

It confirms that the signature is from Alice as we successfully got the message from the signature using Alice’s public key.

Now, if the signature is corrupted, such that the last byte changes from E6 to E5 then, recompiled the program and got the following result:

  

The message is not in the proper hex format, and the output is also not understandable:

 

It proves that if any of the byte is changed in the signature, the whole message is changed and hence proves the authenticity of the message.
Conclusion

In conclusion, completing the given tasks within each of the 4 labs has been extremely beneficial in understanding how cryptography works. It has broadened my knowledge be exploring how a cipher suite is used extensively. This was done through Secret Key Encryption, Pseudo Random Number Generation, MD5 Collision Attack and RSA Public Key Encryption and Signature Lab. For example, it is evident that MD5 collision attacks is relevant in finding two different messages that give the same value. Additionally decrypting and encrypting messages are also crucial skills that need to be applied as seen in Fig. 1 and Fig. 2. It’s vital to be able to understand and apply these technical skills in the IT security industry. 







 
Appendices:

Fig 1:

 









Fig 2:

 


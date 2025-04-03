# TLS Cipher Suites

In this project, I will be showing how I was able to apply my cryptography skills with the labs provided.

### Introduction

Cryptography is a method of encrypting or transforming data into an unreadable format known as cipher text. Cryptography's urgent objective is to discover innovative techniques for producing cryptographic keys at all times. Cryptographers are continually refining and exploring for new ways for generating cryptographic keys in order to successfully accomplish this assignment. This report will focus on labs 1- 4 and I will be focusing on Secret Key Encryption, Pseudo Random Number Generation, MD5 Collision Attack and RSA Public Key Encryption & Signature throughout this report. All these labs were completed on Oracle Box Virtual Machines which will demonstrating all my work I completed throughout this assignment.

---

## Lab 1
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

 ![Screenshot 2025-04-03 at 11 18 10](https://github.com/user-attachments/assets/a1723552-4261-42ea-8a18-5d27af2e461c)


-BF-CBC:
The file plain.txt is encrypted using a salt, password prompt also appears on the terminal during encryption:

 ![Screenshot 2025-04-03 at 11 18 36](https://github.com/user-attachments/assets/23debfb7-70bb-4f14-9ffc-07e8aacfee40)

AES-256-CBC:

 ![Screenshot 2025-04-03 at 11 19 01](https://github.com/user-attachments/assets/366aab6c-5382-4c51-a073-59d12020ff1e)

In this task the pic_original.bmp is encrypted using ECB and CBC encryption. 
The screenshot below highlights the output of the encryption using ECB:

![Screenshot 2025-04-03 at 11 19 57](https://github.com/user-attachments/assets/d0c6ef1c-a45d-4ea8-8e4d-6f69ed6ed57f)
 
Furterhmore, the original header of the pic_original.bmp is replaced by the bogus header of the encrypted file. 

![Screenshot 2025-04-03 at 11 21 41](https://github.com/user-attachments/assets/47041d2c-ad1f-481d-a5ba-e4a663fc2fe2)

As a result, the encrypted file can be viewed by any image viewer. 

 ![Screenshot 2025-04-03 at 11 23 19](https://github.com/user-attachments/assets/bac14543-d8f6-4540-ad97-052a0b77a6e6)

It can identify that the image is still understandable, even after encryption. In addition to this, we will use CBC encryption for the same image.

![Screenshot 2025-04-03 at 11 24 04](https://github.com/user-attachments/assets/5245b278-7213-4711-88e9-12b52ad2babc)

This will allow us to view the encrypted image, which is new_cbc.bmp:

![Screenshot 2025-04-03 at 11 25 26](https://github.com/user-attachments/assets/b145bcc7-16fb-49ed-81a8-15359fc97593)

To conclude with this image, the data is completely masked, and we cannot tell anything about the image. Due to this, CBC encryption is preferred over ECB encryption, which still leaks some information of the image.

---

## Lab 2

#### 2.1 Task:

Random numbers are always required for local key generation and using the best possible ways to get these keys is very important because the information cannot be made as secure as it needs to be. In this lab we will learn wrong way of generating a key and find the problems that can cause problems, as well as the best practices for generating a more secure random key generation.

Description:

The code is copied to the VM and saved as task1.c 

Moreover, will then be compiled using GCC compiler and executed three times. 

![Screenshot 2025-04-03 at 11 43 41](https://github.com/user-attachments/assets/eb05aee3-fdfa-4368-932e-86b464189635)

The output of the program shows the time function and its output with the srand() function. Which means that the output changes with the change in time. Different output for different time values. However, if a person knows the key generation time, they will be able to find the key, whichin turn will make the whole process easily cracked. 

Next the srand () function is commented out and the program is compiled and executed again, as shown:

![Screenshot 2025-04-03 at 11 45 04](https://github.com/user-attachments/assets/0f7d6441-10a7-498b-9947-9cb9241bdb7f)

As a result, the srand() function is not contributing its part in the output, which shows same output each time the program is executed. Because of this, the srand() function is useful in making the output more random in case using it as a key for encryption.


#### 2.2 Task:

The following command is used to watch the output of /proc/sys/kernel/random/entropy_avail continuously on the terminal, as shown:

![Screenshot 2025-04-03 at 11 48 27](https://github.com/user-attachments/assets/02eb5a8b-359b-4ec6-8d11-674ff75260ba)


After observing different operations to test the entropy, it is observed that opening large files and browsing webpages, increases the entropy. While mouse movement has a significant role in increasing the available entropy, because it uses physical world data.

#### 2.3 Task:

In this task the random pool is being observed in real-time, which resides at the location /dev/random, and the output is displayed on the terminal after converting it into hex dump:

![Screenshot 2025-04-03 at 11 49 25](https://github.com/user-attachments/assets/b19c8b65-5765-4029-8074-43da840f40b4)

When all the data is displayed on the terminal the pool gets empty and is blocked, then by moving mouse and clicking on the screen increases the randomness. When the value reaches 63, the command displays another value on the screen by using the randomness from the pool. A hex dump displays 64 bytes of data, so as the decrease in the pool value.

---

### Lab 3

In this lab our task is to create two files with some prefix text, similarly to both files, is to test that whether md5 is collision-resistive or not. 

Description:

To demonstrate the attack, we will use the tool md5collgen. This tool requires a prefix file to create two output files, as shown:

![Screenshot 2025-04-03 at 11 50 15](https://github.com/user-attachments/assets/5060ff88-bcb4-4f92-a68b-6ed3724b3eaf)
 
If we investigate the hashes of the files, these are the same for different files:

![Screenshot 2025-04-03 at 11 51 15](https://github.com/user-attachments/assets/aac82497-1c45-4fc3-933a-65a7c0255733)

By opening each file using the hex editor ‘bless’, we can observe the binary data, as shown:

![Screenshot 2025-04-03 at 11 51 47](https://github.com/user-attachments/assets/b7ec7c86-5ec9-4edc-add4-4c75dd633787)

Both the files contain the same prefix in the beginning of the file while some random data is present in the remaining part of the files, which makes the two files different. Furthermore, the hash must be different but still the hash of the files are same, which opposes the collision-resistance property and makes the hash vulnerable to attacks.

In conclusion this lab proves that md5 hashes are not collision-resistive and allows attackers to use this vulnerability to crack md5 hashes relatively easy.

---

### Lab 4

The purpose of this lab is to demonstrate the use of RSA public key encryption and its usefulness in checking the authenticity of a message. It also demonstrates the results when a signature is corrupted or changed by someone.

Description:
In this lab we will focus on the following tasks:
•	Derive the private key
•	Encrypting a message
•	Decrypting a message
•	Signing a message
•	Verifying a signature

#### Task 1: Derive the private key

	To derive the private key, we will use the program RSATask1.c, which takes the hexadecimal values of p and q and calculates the private key. The program is first compiled using:
		gcc -o Task1 RSATask1.c -lcrypto
  
After running the program, following private key is generated, as shown:

![Screenshot 2025-04-03 at 11 55 20](https://github.com/user-attachments/assets/b03f0d6d-4975-4005-8151-051ed8d2b895)

#### Task 2: Encrypting a Message

The next step is to use the private key to encrypt the message. But the program needs hex code of the message, so the following python command is used to get it:

![Screenshot 2025-04-03 at 11 57 13](https://github.com/user-attachments/assets/57b6a5db-2703-45fd-bc6c-3600f3893c19)

Now, this code will be replaced in the program RSATask2.c and recompiled, to get the encrypted message. The encrypted message is as shown:

![Screenshot 2025-04-03 at 11 57 44](https://github.com/user-attachments/assets/00b62a6f-3083-43b8-8b2e-ed16525f1117)

#### Task 3: Decrypting a Message

In this task we will decrypt the message, that was encrypted in the last task. For this we will replace the encrypted message in the file RSATask3.c and compile it. The following screenshot shows the replaced characters:

![Screenshot 2025-04-03 at 11 58 51](https://github.com/user-attachments/assets/f5b98624-3409-49e1-9e84-b51e7237ac28)

Due to this, I will now execute the file Task3, and the decrypted message will be displayed as shown:

![Screenshot 2025-04-03 at 12 00 12](https://github.com/user-attachments/assets/a5902974-de62-4f02-b09d-e4c6c3019984)

By converting the hex code to plain-text, we can view the actual message, as shown:

![Screenshot 2025-04-03 at 12 01 07](https://github.com/user-attachments/assets/339c6e33-b0ee-4e24-91c4-321fa83ca2ac)

#### Task 4: Signing a message

In this task we will generate a signature for the message, highlighted in the program RSATask4.c, as shown:

![Screenshot 2025-04-03 at 12 07 38](https://github.com/user-attachments/assets/15fae98a-a576-4b88-a88b-20abc95b5271)

The program is compiled and executed in the terminal to get the signature, as shown:

![Screenshot 2025-04-03 at 12 07 49](https://github.com/user-attachments/assets/e581543d-9209-41ff-bc55-73b1229f449a)

Next, we changed the message hex, such that to observe the effect on the signature. The last two characters of the hex code are changed from 21 to 2F, compiled the program, and executed again. Below screenshot shows the output signature of both the messages:

![Screenshot 2025-04-03 at 12 07 58](https://github.com/user-attachments/assets/e354985e-6bf4-468b-ab24-f22cb4d0c939)

This indicates that the signature changes with the change in message and thus keeps the integrity of the message.

#### Task 5: Verifying a signature

Now, the message is received by Bob, with the signature of Alice. To confirm that the message is from Alice, Bob will use Alice’s public key and check its authenticity. 

Open the program file RSATask5.c and add the above signature in place of S, as shown:

![Screenshot 2025-04-03 at 12 11 19](https://github.com/user-attachments/assets/0ce0b4b0-e499-4301-9408-0d55a377a595)

To compile and run then program to get the message in HEX:

![Screenshot 2025-04-03 at 12 12 19](https://github.com/user-attachments/assets/1bb8ef69-51fd-48a2-8e83-8c89e639a357)

To decode the hex to get the original plain text message:

![Screenshot 2025-04-03 at 12 12 36](https://github.com/user-attachments/assets/858d9202-915b-4278-b95a-f50e2a4583c1)

#### Crypto Labs are fun! 

This confirms that the signature is from Alice as I successfully got the message from the signature using Alice’s public key.

Now, if the signature is corrupted, such that the last byte changes from E6 to E5, then recompiled the program and got the following result:

![Screenshot 2025-04-03 at 12 15 06](https://github.com/user-attachments/assets/9936a6ba-ab02-4baa-8cfc-3aa4b42f8eb3)

The message is not in the proper hex format, and the output is also not understandable:

![Screenshot 2025-04-03 at 12 15 29](https://github.com/user-attachments/assets/1f88f27d-90bd-4533-86f6-d2266c261e39)

This verifys that if any of the byte is changed in the signature, the whole message is changed and hence proves the authenticity of the message.

---

### Conclusion

In conclusion, completing the given tasks within each of the 4 labs has been extremely beneficial in understanding how cryptography works. It has broadened my knowledge be exploring how a cipher suite is used extensively. This was done through Secret Key Encryption, Pseudo Random Number Generation, MD5 Collision Attack and RSA Public Key Encryption and Signature Lab. For example, it is evident that MD5 collision attacks is relevant in finding two different messages that give the same value. Additionally, decrypting and encrypting messages are also crucial skills that need to be applied. It’s vital to be able to understand and apply these technical skills in my opinion. 


 


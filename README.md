# Project: Steganography-Tools
# Made by - Koustubh Sinha
# Introduction
Steganography is the art of hiding the fact that communication is taking place, by hiding information in other information. Steganography is the practice of concealing a message within another message or a physical object. In computing/electronic contexts, a computer file, message, image, or video is concealed within another 
file, message, image, or video.

In this project hides the message with in the image, text file, audio file and video file. In this project, the sender selects a cover file (image, text, audio or video) with secret text and hide it into the cover file by using different efficient algorithm and generate a stego file of same format as our cover file (image, text, audio or video). Then the stego file is sent to the destination with the help of private or public communication networks. On the other side i.e. receiver, the receiver downloads the stego file and by using the appropriate decoding algorithm retrieves the secret text that is hidden in the stego file.

![Screenshot 2022-10-27 225540](https://user-images.githubusercontent.com/54525819/198358124-9540922e-d636-4da2-9d5d-fed9bb06c5ed.png)


## Text Steganography

We hide text in a text file using, ZWCs.
ZWCs-ZWCs- In Unicode, there are specific zero-width characters (ZWC) that are used to control special entities such as Zero Width Non Joiner (e.g., ZWNJ separates two letters in special languages) and POP directional, which have no written symbol or width in digital text.

![Screenshot 2022-10-27 233856](https://user-images.githubusercontent.com/54525819/198366474-46dd1e30-076a-474c-9341-9824413c9b35.png)

* We get its ascii value and it is incremented or decremented based on if ascii value between 32 and 64 , it is incremented by 48(ascii value for 0) else it is decremented by 48.
* Then xor the the obtained value with 170(binary equivalent-10101010) .
* Convert the obtained number from first two step to its binary equivalent then add "0011" if it earlier belonged to ascii value between 32 and 64 else add "0110" making it 12 bit for each character.
* With the final binary equivalent we also 111111111111 as delimiter to find the end of message.
* Now from 12 bit representing each character every 2 bit is replaced with equivalent ZWCs according to the table. Each character is hidden after a word in the cover text.


## Image Steganography

In this we hide text message in an image file, using Modified LSB Algorithm where we overwrite the LSB bit of actual image with the bit of text message character. At the end of text message we push a delimiter to the message string as a checkpoint useful in decoding function. We encode data in order of Red, then Green and then Blue pixel for the entire message.


## Audio Steganography

We will be using Cover Audio as a Cover file to encode the given text. Wave module is used to read the audio file. Firstly we convert our secret message to its binary equivalent and added delimiter '*****' to the end of the message. For encoding we have modified the LSB Algorithm, for that we take each frame byte of the converting it to 8 bit format then check for the 4th LSB and see if it matches with the secret message bit. If yes, change the 2nd LSB to 0 using the logical AND operator between each frame byte and 253(11111101). Else we change the 2nd LSB to 1  using logical AND operation with 253 and then logical OR to change it to 1 and now add secret message bit in LSB for achieving that use logical AND operation between each frame byte of carrier audio and a binary number of 254 (11111110). Then logical OR operation between modified carrier byte and the next bit (0 or 1) from the secret message which resets the LSB of the carrier byte.


## Video Steganography

In video steganography we have used combination of cryptography and Steganography. We encode the message through two parts:-
* We convert plaintext to cipher text for doing so we have used RC4 Encryption Algorithm. RC4 is a stream cipher and variable-length key algorithm. This algorithm encrypts one byte at a time. It has two major parts for encryption and decryption:-
* KSA(Key-Scheduling Algorithm)- A list S of length 256 is made and the entries of S are set equal to the values from 0 to 255 in ascending order. We ask user for a key and convert it to its equivalent ascii code. S[] is a permutation of 0,1,2....255, now a variable j is assigned as j=(j+S[i]+key[i%key_length) mod 256 and swap S(i) with S(j) and accordingly we get new permutation for the whole keystream according to the key.
* PRGA(Pseudo random generation Algorithm (Stream Generation)) - Now we take input length of plaintext and initiate loop to generate a keystream byte of equal length. For this we initiate i=0, j=0 now increment i by 1 and mod with 256. Now we add S[i] to j amd mod of it with 256 ,again swap the values. At last step take store keystreambytes which matches as S[(S[i]+S[j]) mod 256] to finally get key stream of length same as plaintext.
* Now we xor the plaintext with keystream to get the final cipher.


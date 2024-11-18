+++
title = 'NGLCTF24_writeup'
date = 2024-11-18T22:59:40+06:00
draft = false
tags = ['NGLCTF24']
categories = [ 'Writeups',]
[comment]
    enable = true
+++

##Crypto
Most of the Crypto problems given in this ctf can be solved using https://www.dcode.fr/ or CyberChef. We can identify chipher from https://www.dcode.fr/cipher-identifier.

### Basic Rule:
    - `Uniform India Tango Sierra {Delta Alfa Mike Mike !_Yankee Oscar Uniform _Alfa Romeo Echo _Papa Romeo Zero Zero !!_Hotel Alfa Charlie Kilo Echo Romeo !!!}`
    - This one is [NATO Phonetic Alphabet](https://www.dcode.fr/nato-phonetic-alphabet). 
    Decrypting it given: `U I T S D A M M Y O U A R E P R 0 0 H A C K E R `.
    - **BUT** If we look at the text closely, we can actually do it without using any tool. Just taking every capital letter inside the curly braces gives us the flag. Also we need all those '!'. 
    - flag: `NGLCTF24{Damm!_You_Are_Pr00!!_Hacker!!!}`

### AFFA 
    - `MGFY{Fzcpuy_70_Cllgpe_Qgdzer}`
    - Identifier and Challenge Name suggests its: Affine Cipher
    - Decrypting with it gives us the flag: `UITS{Thanks_70_Affine_Cipher}`.
    
### Cease All Your Fire 
    - `XLWV{Kdfn_Wkh_zruog_zlwk_FHDVHU}`
    - Identifier and Challenge Name suggests its: Caesar Cipher
    - Decrypting with it gives us the flag: `UITS{Hack_The_world_with_CEASER}`.

### [Fo]R[g]oTTeN 
    - `HVGF{E52_6F_E5XXXXX0000}`
    - From Challenge Name and Description we can deduce its some form of ROT Cypher.
    - I did it with CyberChef, where with ROT13 it gives us something which looks like a flag. But actually a attempt eater trap.
    - Then I tried rotate number and increasing the Amount of rotation and eventually got something at ROT65 which kinda make more sense. 
    - flag: `UITS{R07_1S_R0KKKKK5555}`

### Hiji Biji 
    - This onne give us a text file.
    - The text inside seemed like some kind of Base so I gave it to CyberChef. Rest is CyberChef Magic and we get the flag. 😆 
    - flag: `UITS{Time_is_Honey!!!:PP}`

### Fresh!! 
    - The png file shows us hand sign. Searching decodefr with hand/handsign gave American Sign Language (hand) and that was kind of a mistake. Missed the challenge name clue. But luckly decodefr similar cipher was suggesting French Sign Language. Putting all the sign gave the flag, and we got to know Q99 bro likes French Women, huh...
    - flag: 
    
### Heart Beat 
    - Tried searching heart, beat, electric etc. but none helped. Then tried google image search and got some result. "The Tenctonese alphabet" Searching and putting signs to decodefr got the flag.
    - flag: 
    
### Everything is **UCK 
    - Identifier and Challenge Name suggests its: Alphuck
    - flag: `UITS{i_am_too_sleeeepyyyy}`

### Language of F!sh 
    - Deadfish Language  (decrypting with ASCII character option)
    - flag: `UITS{Fish_0r_PHISH_you_have_been_hacked!!haha}`
    
### Daenerys Targaryen 
    - Searching with  Daenerys or Drago gives us Dothraki Alphabet.
    - Decryption resulted: `ISHRAQLOVEDTHEGAMEOFTHRONESERIESS`
    - flag: `NGLCTF24{ishraq_loved_the_game_of_thorne_seriess}`
    
###  2x + 2x = flag
    - `1h55cj6gj1oy1na5ly1b959w5x01jk1cj4u11eg63953o1lw68l53o1p316o`
    - Twin Hex Cipher - as hinted in challenge name we gotta do it 2 times.
    - 'UITS{2x_2x_=_FLAG_hahaha}' which should be the flag, but flag format complication makes it `NGLCTF24{2x_2x_=_FLAG_hahaha}`.


## Forensic

### Extension 
    - This one can be done using file command in linux terminl. $`file who-am-i` shows the result: `who-am-i: Zip archive data, made by v2.0 UNIX, extract using at least v2.0, last modified, last modified Sun, Nov 13 2024 03:01:08, uncompressed size 71878, method=deflate`
    - flag: NGLCTF24{zip}

### Hidden 
    - This one is on the same file. File command shows that it's a zip file. So, tried extracting but that failed due to zip file being currupted. 
    - Then `hexdump -C who-am-i | head` showed that file hex signature head is `0000000  9e 69 00 50 14 00 08 00  08 00 24 18 6d 59 00 00  |.i.P......$.mY..|` which should actually be `50 4B 03 04`. 
    - List of signature is here: https://en.wikipedia.org/wiki/List_of_file_signatures
    - So, edited (replaced) `9e 69 00 50` portion with correct `50 4B 03 04`  and fixed the signature. All using Octeta hex editor.
    - Then extracting the fixed zip file, got a jpg image named who-am-i.jpg
    - Checking its Metadata using $`exiftool who-am-i.jpg` got a comment:
    ```bash
    Comment                         : 64 145 40 64 67 40 64 143 40 64 63 40 65 64 40 64 66 40 63 62 40 63 64 40 67 142 40 64 144 40 63 63 40 67 64 40 63 64 40 66 64 40 63 64 40 67 64 40 63 64 40 65 146 40 65 65 40 66 145 40 66 143 40 63 60 40 66 63 40 66 142 40 63 63 40 66 64 40 65 146 40 65 63 40 67 65 40 66 63 40 66 63 40 63 63 40 67 63 40 67 63 40 66 66 40 67 65 40 66 143 40 66 143 40 67 71 40 65 146 40 64 64 40 63 63 40 66 63 40 66 71 40 67 60 40 66 70 40 66 65 40 67 62 40 63 63 40 66 64 40 67 144

    ```
    - Putting the comment text in CyberChef yielded the flag: `NGLCTF24{M3t4d4t4_Unl0ck3d_Succ3ssfully_D3cipher3d}`

## Web

### Somthing left behind
    - Inspected the web page
    - Should've guess that it's in the comment from the Challenge name. but didn't.
    - Yeah, it's on the last line comment -'<!-- hiding my secrets: EKO{s1mpl3_comm3nt} -->'
    - flag: `NGLCTF24{s1mpl3_comm3nt}`

## Steganography

### Sweet Crush 
    - This one gives us a text file containing a super big single line string.
    - Dropping the whole file in CyberChef gave a line of numbers.
    - Seems like hex valus. Selecting 'From Hex' in CyberChef. CyberChef magic icon poped up and clicking it we got a Image containing the flag.
    - flag: `NGLCTF24{In_the_depths_of_encoding_you_found_the_hidden_artifact_transcending_base64_into_visual_clarity}`
    

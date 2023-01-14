---
layout: post
title: "My experience in Sieberrsec 4.0"
date: 2023-1-14 19:50:00 +0800
categories: jekyll update
---

> The official website for Sieberrsec can be found [here.](https://sieberrsec.live/)
> <br/>
> Sieberrsec CTF 4.0 is a Cybersecurity Jeopardy-Style Capture-The-Flag Competition for Junior College and Secondary school students and is organised by the Hwa Chong Institution Infocomm and Robotics Society's Cybersecurity Section, also known as Sieberrsec.

# My history with Sieberrsec
I have participated in Sieberrsec for about 2 to 3 years by this point, usually alone. I usually ranked 30-40 on the leaderboard and manage to complete about a third of the challenges. However, this year was the first time I played the CTF with a partner, given that the maximum team size this year is 2.

# General account of events
Sieberrsec this year was a 15 hour event, and was an online event just like in previous years. I lack experience at CTFs, so I tried to focus on miscellanious challenges and reverse engineering challenges (we managed to solve both challenges), while my partner helped me solve OSINT and web exploitation challenges that I kept stumbling on. Since I got lucky and managed to solve a bunch of challenges that gave many points, we managed to close in at 18<sup>th</sup> place out of about 80+ competitors, with out highest ever rank being 15<sup>th</sup> place. We also solved about a third of the challenges again.

## Challenges that I solved personally (note that challenge names are inexact)

# My First Calculator

> The writeup for this challenge can be found [here.](/jekyll/update/2023/01/14/SEIBERRSEC-MY-FIRST-CALCULATOR.html)

# Siebersat

Netcatting to the challenge server results in me recieving a corrupted binary string. The key insight is that bits in different positions are chosen to be flipped each time, so by collecting enough binary strings you can determine which bits should stay the same.

# Quick Maths

Netcat to the challenge server and recieve a series of many math questions to solve. Problem is, you must do them very quickly, so essentially this challenge was about writing a script. I ended up using a Python library called **nclib** and figuring out how to use it consumed quite a few hours of my time.
> What was worse was that incorrect instructions were given. The challenge states that answeres should be rounded down to the nearest integer, but it turned out you had to _truncate_ the decimal part instead.

# Infant RSA

There were a bunch of RSA-related challenges that I solved by simply using **RsaCtfTool**. However, this one was slightly different.

**p** and **q** were not given, instead I was given **x = (p-1)q**, **y = (q-1)p** and **n = pq**. I was stuck on this, but I realised I could use the Greatest Common Divisor (GCD) Python function to recover **p** and **q**, since **GCD(x, n) = q** and **GCD(y, n) = p**.

# Fast Fourier Transform (I can't remember the actual name but it alluded to the concept of FFT)

I couldn't explain what FFT is, but I had watched [Veritasium's video on the subject](https://www.youtube.com/watch?v=nmgFG7PUHfo) and I immediately knew what was up.
The challenge involved multiplying 2 polynomials together, and in order to perform such an operation in a resonable amount of time, you had to use an algorithm that used FFT. I did not have the luxury of time to actually understand what actually went on behind the scenes, but I managed to find [this library](https://gist.githubusercontent.com/ksenobojca/dc492206f8a8c7e9c75b155b5bd7a099/raw/dfdfa951983943f8fe346efb2cdf9bef06afbcfd/fft.py) that did exactly what I needed it to do.

# Encoding Fever

I was given a ciphertext that was basically just a string that was encoded in base85 multiple times. Given that base85 is such a rare encoding, the real challenge was finding the right encoding standard but Python's ```base64.b85decode``` did the trick.

# Do You Remember? 1 and 2

I was given a memory dump to retrieve certain pieces of data out of. For this, I had to use the program **Volatility**, but I struggled initially with tracking down a copy of it. First, I had to use the command ```kdbgscan``` to determine the memory dump's OS profile, since certain commands failed on it due to the dump's OS profile.

I was tasked to extract a string typed in Notepad, and that involved using the command ```psscan``` to determine Notepad's ID, and than extracting the relevant parts of the memory and using the terminal command **strings** to find the flag.

Next, I had to find a drawing made in paint and a password. Extracting images from the memory dump involved me improting it into GIMP and messing around with the offset on the output image until the flag could be seen. The password involved using ```hivescan``` to extract the password hash from the right reigstry hive, nd the cracking the hash with **hashcat**.
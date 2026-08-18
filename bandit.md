#### level 0:
commaand: sudo ssh bandit0@bandit.labs.overthewire.org -p 2220

#### level 0 --> level 1:
pw: 6y2kwnwK6grgvwvpvLaa2T1cpFEKOhNR

#### level 1 --> level 2:
command: cat ./-

pw: PK8fYLZg2hnHSz83plBL1iEPKdD3QToB

#### level 2 --> level 3:
command: cat -- "--spaces in this filename--"

reason: the first -- makes everything after a filename, not as an option or a flag.

pw: 7ZZ2LFrykP2zEyvBl4m3clcL7tGYJPME

#### level 3 --> level 4:
command: cd inhere --> find --> cat ./...Hiding-From-You

pw: xzTXq1rDJQVVAzdv5cHq1TQytTWufAMq

#### level 4 --> level 5:
command: cat -- -file07

pw: 6C7h9GD8M6ai5nr7wo1RonrzFjj9yIrG

#### level 5 --> level 6:
command: find -size 1033c ! - executable -readable

lesson: there were multiple directories with numerous files in each one, so trying to discover the password by manually going through each one would be time consuming. I used 'man find' to go through the manual and discovered how to narrow down the search, by listing the requirements for the file.

pw: pXa26xhMWaC2SvDotA4r9EgZkulOeSBW

#### level 6 --> level 7:
command: find / -type f -user bandit7 -group bandit6 -size 33c 2>/dev/null

lesson: I learnt two new things - '/' after find starts the search point in the whole system. when trying to execute the command above without '2>/dev/null' the terminal was flooded with permission denied messaged, this was beacuse find goes through every directory and since i would be an underprivileged user i was denied - why there was error messages. '2>/dev/null' ignores all the error messages and presents successful matchings.

pw: Bmnnvf82KzQlfxgAI2d1zYbr1u9pr3E3

#### level 7 --> level 8:
command: grep "millionth" data.txt

pw: VR1ljMayciFxbnUokuQmJFw6QC9VKtub

#### level 8 --> level 9:
command: sort data.txt | uniq -u

lesson: learning pipping '|' and what it does, from what i learnt it is a way to combine to commands together - passing from left to right. In this level, I used it to sort out a file and print out a string that hasn't been repeated and shown once.

pw: EjmOSvuAu7sGAHqHVcBDPirRe9T03kxl

#### level 9 --> level 10:
command: strings data.txt | grep "="

mistake: i first use cat to read the file and it presented alot of unreadable text, i then use base64 because i thought it would decode the file, but it was a data file so it presented errors. 

lesson: using pipping again and making the data file into a strings file and then use grep to find any lines with '='

pw: B0s2khmbT9u0geKuOoVGW3JZKhndE3BG

### level 10 --> level 11:
command: base64 -d data.txt

lesson: using the link provided by OverTheWire and reading through the manual, base64 decode/encodes data. Using the '-d' option alongside it decodes the selected file after.

pw: pYfOY6HwUsDj5rL9UvyhU7MCmv8vN5Ro

### level 11 --> level 12:
command: tr 'A-Za-z' 'N-ZA-Mn-za-m' < data.txt

mistakes: i was trying to use the command sort to try reorganise the file, but discovered a command 'tr' which translates or deletes characters.

lesson: Using redirection learnt from previous levels and the link provided by OTW, I was able to execute the correct command to get the pw for the next level.

pw: GROozWPO8QyN0mGrjUkID0WCYkZiQxrN

### level 12 --> level 13:
commands:

```bash
#doing what OTW says to do
mktemp -d
cd /tmp/tmp.Vogruso8e8

#reverse the hexdump back into binary
xxd -r data.txt > data.decoded

#identifying file type
file data.decoded

#this will be explained later on, depending on file type, decompress
mv data.decoded data.gz && gunzip data.gz #if gzip 
mv data.decoded data.bz2 && bunzip2 data.bz2 #if bzip2
mv data.decoded data.tar && tar -xf data.tar #if tar

#until file type is ASCII, repeat
file data
cat data
```

lesson: to discover the password in this level, I had to learn about reverse hexdumps and decompress files depending on the file type to make it an ASCII file type so it is readable. This level wasn't done alone, but with the use of AI as it became quite confusing when it got to decompressing section and doing it continously until the right file type was made.

pw: qQYQiHOBPR8zR61qxYqX45quvihF2uzk

### level 13 --> level 14:
commands:
```bash
#copying the private key from bandit 13 to my home directory
scp -P 2220 bandit13@bandit.labs.overthewire.org:sshkey.private .   

#adding permissions to the private key, so it can be used
sudo chmod 700 sshprivate.key

#ssh into bandit14 with the private key
ssh -i sshkey.private bandit14@bandit.labs.overthewire.org -p 2220

#reading the file listed in OTW
cat /etc/bandit_pass/bandit14
```

lesson: This level taught SSH key-based authentication as an alternative to passwords, including how private key file permissions are enforced by SSH for security, and how to securely transfer files between hosts using scp.

pw: aaWecNkG4FhxJQxz07uiwzVP6bJiYS65

### level 14 --> level 15:
commands:
```bash
#within level14, connect to the local host
nc localhost 30000

#entering the password to level 14, password for level 15 should appear
```

lesson: understanding what nc (netcat) does, opening a raw connection. Discovered this is used by attackers frequently, so understanding how it works and what it can be used for, will be important for a blue-team.

pw: pbLYuZtTg4MgaqfJx8jbA9gKKGqM68A7

### level 15 --> level 16:
commands:
```bash
#connecting to port 30001 on localhost using SSL/TLS encryption
openssl s_client -connect localhost:30001
```

mistakes: I was treating it the same as nc and it was just creating errors, discovered it was the way i was writing localhost, the port and missing '-connect'

lesson: the difference between SSL/TLS and nc, a brief understanding of TLS handshake, what it looks like to have a successful connection and how to execute it.

pw: kS0Hf0u5HiXFwKMKFqXvPdOTNGGa0X8V

### level 16 --> level 17:

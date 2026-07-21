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

lesson: learning pipping '|' and what it does, from what i learnt it is a way to combine to commands together - passing from left to right. In this level, I used it to sort out a file and print out a string that hasn't benn repeated and shown once.

pw: EjmOSvuAu7sGAHqHVcBDPirRe9T03kxl

#### level 9 --> level 10:
command: strings data.txt | grep "="

mistake: i first use cat to read the file and it presented alot of unreadable text, i then use base64 because i thought it would decode the file, but it was a data file so it presented errors. 

lesson: using pipping again and making the data file into a strings file and then use grep to find any lines with '='

password: B0s2khmbT9u0geKuOoVGW3JZKhndE3BG

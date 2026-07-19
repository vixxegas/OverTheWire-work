level 0:
commaand: sudo ssh bandit0@bandit.labs.overthewire.org -p 2220

level 0 --> level 1:
pw: 6y2kwnwK6grgvwvpvLaa2T1cpFEKOhNR

level 1 --> level 2:
command: cat ./-
pw: PK8fYLZg2hnHSz83plBL1iEPKdD3QToB

level 2 --> level 3:
command: cat -- "--spaces in this filename--"
reason: the first -- makes everything after a filename, not as an option or a flag.
pw: 7ZZ2LFrykP2zEyvBl4m3clcL7tGYJPME

level 3 --> level 4:
command: cd inhere --> find --> cat ./...Hiding-From-You
pw: xzTXq1rDJQVVAzdv5cHq1TQytTWufAMq

level 4 --> level 5:
command: cat -- -file07
pw: 6C7h9GD8M6ai5nr7wo1RonrzFjj9yIrG



---
layout: post
title: Auto Confirm in Command
---
In spirit learning bash script, I tried to clone "yes" command which recursively send character "y" (by default) as input for next command.
```bash
yes | next_command # how to use it, or
yes character | next_command # if want to send custom character
```
and if you run "yes" alone, it will print
```bash
yes
yes
yes
# will print yes forever until got killed
```
"yes" is usefull when you need to auto-answer with y/yes/n/no/or any characters you want. 

For this, we are only need to echo character "nay" recursively.

Simplest bash script will look like this:
```bash
while true; do
	echo "nay"
done
```
And it will fulfill simple testing like:
```bash
sh nay.sh 
nay
nay
nay
# will print forever until got killed
```
To make it usefull, then we need to give it capability to accept other character. It could be easily implemented with `$#`.
```bash
ANSWER="nay"
if [ $# -eq 1 ]; then
	ANSWER=$1
fi

while true; do 
	echo $ANSWER
done
```

Now, we could use it for auto confirming, i.e:
```bash
# I save my script as nay.sh
sh nay.sh y | rm -i text*.txt
```

# Extra Notes
"yes" command actually implemented in c in unix-based OS ([wiki link](https://en.wikipedia.org/wiki/Yes_(Unix)))

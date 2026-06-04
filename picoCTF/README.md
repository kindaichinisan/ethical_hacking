# Base64 encoding
binary -> groups of 6bits  
group of 3 Byte (24 bits)
Base64 usually contains:
- A-Z (0 to 25)
- a-z (26 to 51)
- 0-9 (52 to 61)
- + (62)
- / (63)
- sometimes = (for padding)
strlen is normally divisible by 4 (4*6=24)  
14 bit will be padded to 16 bit (2Byte) with leading 0. Then for last Byte, replace with = to make it 3 Byte  
Assume input is multiple of 8 bit (1 Byte)  

# Hex encoding
Contains:
- 0-9
- a-f or A-H

# Binary encoding
Contains 0, 1

# strings executable
xtracts human-readable text from binary file.  
Even though executable is machine code, text strings inside it are still stored as plain bytes.  
use strings <bin> | grep picoCTF

# Inspect webpage
Inspect html, css, javascript in website.

# grep
grep -o "picoCTF{.*}" file: find string of the following form  
-o: print only matching part
.*: any characters (greedy)

# robots
robots.txt is a plain text file located at the root of a website. It provides instructions for web crawlers (often used by search engines) on which parts of the website they can access.  
Interpreting the robots.txt output  
The file might contain a line like `disallow: /path/to/restricted/file.html`. This indicates a specific path on the website that the crawler should not access. Following the Disallowed Path

# rmdir non-empty directory
rmdir <foldername> is strictly for empty folder.  
rm -rf <foldername>: -r tells sys to delete directory and everything inside. -f (force) ignores non-existent files and never prompts for confirmation.

# write a for loop in bash
write a for loop in bash to try out password  
for pwd in "9f63"; do echo "$pwd" | python3 level4.py; done

# read password from a file
while read pwd; do
    echo "$pwd" | python3 level4.py
done < passwords.txt  
need to read the py code carefully as it will not break after finding the password.

In order to break, use the following code  
while read pwd; do     res=$(echo "$pwd" | python3 level5.py); if echo "$res" | grep -q "Welcome"; then     echo "$pwd"; break; fi done < dictionary.txt

# find hidden msg in image
use cat or strings <imgfilename>
picoCTF{3nh4nc3d_24374675}

# Use grep to find in directory inside file
grep -r -o "picoCTF{.*}" big-zip-files

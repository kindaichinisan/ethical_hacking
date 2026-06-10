# Obedient Cat (General skills, easy)
Download the file and open in Notepad. The answer will be there.

# Super SSH (General skills, easy)
Use putty to SSH
Hostname: titan.picoctf.net
Port: 62739
Close window on exit: Never
login as: ctf-player
password: 1db87a14
Learning: learn how to use ssh in putty.

# what's a net cat? (General skills, easy)
Use kali-linux
nc fickle-tempest.picoctf.net 57648
Learning: netcat is used to read and write data across network connection using TCP or UDP protocol. It is often referred to as Swiss Army knife of networking.
nc [options] [hostname] [port]
options:
-l: listen (server). If never put, means it is client.
-p <portnum>: port
-v: verbose
-w <num_sec>: wait # sec b4 terminating the connection
> <txtfile>: server to receive and save the file.
< <txtfile>: client to send the file indicated in txtfile
-u: establish UDP connection. By default, netcat uses TCP connection.
-n: to connect to numerical IP address, not a domain name.

# Mod 26 (Cryptography, easy)
Use https://cryptii.com/pipes/rot13-decoder/
Enter into ciphertext. Then ROT13 decode to get the plain text.  
Rotate by 13 places. Is symmetric.
If letter, maintain case and shift by 13 with wrapback.
If number, dont change.

# Warmed Up (General skills, easy)
What is 0x3D (base 16) in decimal (base 10)?  
Convert from hex to decimal. Wrap inside picoCTF{}.

# 2warm (General skills, easy)
Can you convert the number 42 (base 10) to binary (base 2)?  
Convert from decimal to decimal. Wrap inside picoCTF{}.

# Bases (General skills, easy)
What does this bDNhcm5fdGgzX3IwcDM1 mean? I think it has something to do with bases.  
It is Base64. Decode using Base64. Wrap inside picoCTF{}.
binary (pad to 24 bits) -> 4 groups of 6bits  
Base64 ciphertext usually contains:
- A-Z (0 to 25)
- a-z (26 to 51)
- 0-9 (52 to 61)
- + (62)
- / (63)
- sometimes = (for padding). If the 6-bit is fully padding, it is encoded as "=" instead of "A".  
If 0 "=" in ciphertext (original plaintext len<=24 bit), original data is 3 Byte.  
If 1 "=" in ciphertext (original plaintext len<=24-1*6=18 bit), original data is 2 Byte.  
if 2 "=" in ciphertext (original plaintext len<=24-2*6=12 bit), original data is 1 Byte.  
if 3 "=" in ciphertext (original plaintext len<=24-3*6=6 bit), not possible.  

# Wave a flag (General skills, easy)
Can you invoke help flags for a tool or binary? This program has extraordinarily helpful information...  
Use Ubuntu.  
./warm --help does not work
./warm -h

# Tab, Tab, Attack (General skills, easy)
Using tabcomplete in the Terminal will add years to your life, esp. when dealing with long rambling directory structures and filenames.  
unzip zipped file.  
cd tab tab tab tab tab tab ...
ls
./fang-of-haynekhtnamet
Learning point: use cd tab tab if folder only has 1 file/ folder inside.  

# Insp3ct0r (Web exploitation, easy)
Kishor Balan tipped us off that the following code may need inspection:  
Open website
Inspect > Elements tab > Ctrl + F > picoCTF to find <!-- Html is neat. Anyways have 1/3 of the flag: picoCTF{tru3_d3 -->
Ctrl + P > mycss.css > /* You need CSS to make pretty pages. Here's part 2/3 of the flag: t3ct1ve_0r_ju5t */
Ctrl + P > /* Javascript sure is neat. Anyways part 3/3 of the flag: _lucky?302945a7} */

# strings it (General skills, easy)
strings strings | grep picoCTF
Cannot use grep -o "picoCTF{.*}" strings as strings is a binary file instead of text file.
strings <bin_file>: Extracts human-readable text from binary file.  
Even though executable is machine code, text strings inside it are still stored as plain bytes.  
use strings <bin> | grep picoCTF
grep assumes:
- input is text
- lines are separated by \n
- data is stable character encoding (consistent sequence of characters. Each byte corresponds to readable characters. UTF-8 / ASCII)

# First Grep (General skills, easy)
strings strings | grep picoCTF will show picoCTF in red. But need to find in the long string.: strings file → extracts all printable ASCII strings from a binary file. grep picoCTF → filters those strings. grep picoCTF filters it down, but since the flag is inside a big blob, you still see surrounding context.
grep -o "picoCTF{.*}" file: Directly searches the file for regex match. -o prints only matching part

# where are the robots (Web exploitation, easy)
Go to website.  
Add /robots.txt
    User-agent: *
    Disallow: /cc6b1.html
Add /cc6b1.html to website.

# Python Wrangling (General skills, medium)
Anaconda Prompt.
Read ende.py to understand how to run it.
sys.argv[0]=ende.py
sys.argv[1]=-d
sys.argv[2]
sys.argv[3]
python ende.py -d flag.txt.en or
python ende.py -d flag.txt.en 720b6ad346f84cd483c60c7464dd95d4
Type password 720b6ad346f84cd483c60c7464dd95d4 from password.txt
sim_sala_bim.encode(): Converts the string into bytes using UTF-8 (default encoding)
base64.b64encode(...): Encodes those bytes into Base64.
c = Fernet(ssb_b64): This creates a Fernet encryption object using a key stored in ssb_b64

# PW Crack 1 (General skills, easy)
Can you crack the password to get the flag?
Download the password checker here and you'll need the encrypted flag in the same directory too.
Read the level1.py to find that the password is hardcoded inside. 8713
python level1.py
Type password 8713.

# PW Crack 2 (General skills, easy)
Read the level2.py to find that the password is hardcoded inside.
chr(0x64) + chr(0x65) + chr(0x37) + chr(0x36) = de76 (looks at ascii table)
chr(number)->character (ascii/unicode)
ord(character)->number
unicode 0-127 is exactly the same as ASCII
8-bit ascii is extended ASCII but there is no single universal 8-bit ASCII standard (many incompatible version).
Today, we use UTF-8.
UTF-8 is a variable-length encoding (1 byte for basic ASCII, 2–4 bytes for other characters) that converts Unicode characters into 1–4 bytes, while preserving ASCII compatibility.
Unicode defines characters; UTF-8 is one way to encode Unicode into bytes.
UTF-16 encodes Unicode using 2 bytes for most characters and 4 bytes for rare ones outside the Basic Multilingual Plane.
UTF-32 encodes every Unicode character using a fixed 4-byte representation, making it simple but memory-inefficient.
UTF-8 and UTF-16 are different encoding for unicode characters.

# PW Crack 3 (General skills, medium)
Read the level3.py
Can brute force the 7 password and try all 7.
Alternatively, modify the level3.py level_3_pw_check()
def level_3_pw_check():
    
    print(f"correct_pw_hash: {correct_pw_hash}")
    pos_pw_list = ["6997", "3ac8", "f0ac", "4b17", "ec27", "4e66", "865e"]
    
    for pos_pw in pos_pw_list:
        print(f"{pos_pw}: {hash_pw(pos_pw)}")

    user_pw = input("Please enter correct password for flag: ")
    user_pw_hash = hash_pw(user_pw)
    
    print(f"user_pw_hash: {user_pw_hash}")
    if( user_pw_hash == correct_pw_hash ):
        print("Welcome back... your flag, user:")
        decryption = str_xor(flag_enc.decode(), user_pw)
        print(decryption)
        return
    print("That password is incorrect")

# PW Crack 4 (General skills, medium)
Modify level4.py to use for loop to find the password that matches the hash.
def level_4_pw_check():
    pos_pw_list = ["8c86", "7692", "a519", "3e61", "7dd6", "8919", "aaea", "f34b", "d9a2", "39f7", "626b", "dc78", "2a98", "7a85", "cd15", "80fa", "8571", "2f8a", "2ca6", "7e6b", "9c52", "7423", "a42c", "7da0", "95ab", "7de8", "6537", "ba1e", "4fd4", "20a0", "8a28", "2801", "2c9a", "4eb1", "22a5", "c07b", "1f39", "72bd", "97e9", "affc", "4e41", "d039", "5d30", "d13f", "c264", "c8be", "2221", "37ea", "ca5f", "fa6b", "5ada", "607a", "e469", "5681", "e0a4", "60aa", "d8f8", "8f35", "9474", "be73", "ef80", "ea43", "9f9e", "77d7", "d766", "55a0", "dc2d", "a970", "df5d", "e747", "dc69", "cc89", "e59a", "4f68", "14ff", "7928", "36b9", "eac6", "5c87", "da48", "5c1d", "9f63", "8b30", "5534", "2434", "4a82", "d72c", "9b6b", "73c5", "1bcf", "c739", "6c31", "e138", "9e77", "ace1", "2ede", "32e0", "3694", "fc92", "a7e2"]
    
    for pos_pw in pos_pw_list:
        if hash_pw(pos_pw) == correct_pw_hash:
            print("The correct password is: " + pos_pw)
            break
    user_pw = input("Please enter correct password for flag: ")
    user_pw_hash = hash_pw(user_pw)
    
    if( user_pw_hash == correct_pw_hash ):
        print("Welcome back... your flag, user:")
        decryption = str_xor(flag_enc.decode(), user_pw)
        print(decryption)
        return
    print("That password is incorrect")

# PW Crack 5 (General skills, medium)
There are 16^4=65536 passwords to try. Modify the python file to read from file and hash to find the correct password.
def level_5_pw_check():

    with open("dictionary.txt", "r") as f:
        for line in f:
            if hash_pw(line.strip()) == correct_pw_hash:
                print("Found password in dictionary: " + line.strip())
                break

    user_pw = input("Please enter correct password for flag: ")
    user_pw_hash = hash_pw(user_pw)
    
    if( user_pw_hash == correct_pw_hash ):
        print("Welcome back... your flag, user:")
        decryption = str_xor(flag_enc.decode(), user_pw)
        print(decryption)
        return
    print("That password is incorrect")

This method is very slow (run >1min) compared to the modify python file method (run w/i a sec).
while read pwd; do
    echo "$pwd" | python3 level4.py
done < passwords.txt  
need to read the py code carefully as it will not break after finding the password.

In order to break, use the following code  
while read pwd; do     res=$(echo "$pwd" | python3 level5.py); if echo "$res" | grep -q "Welcome"; then     echo "$pwd"; break; fi done < dictionary.txt

# Enhance! (Forensics, medium)
Download this image file and find the flag.
strings drawing.flag.svg
The only difficulty of this challenge is to realise that the flag was split into different parts. All we have to do is join “p”, “i”, “c”,“o”, “C”, “T”, “F { 3 n h 4 n ” and “c 3 d _ 2 4 3 7 4 6 7 5 }” and we have our flag. picoCTF{3nh4nc3d_24374675}
        id="tspan3748">p </tspan><tspan
         sodipodi:role="line"
         x="107.43014"
         y="132.08942"
         style="font-size:0.00352781px;line-height:1.25;fill:#ffffff;stroke-width:0.26458332;"
         id="tspan3754">i </tspan><tspan
         sodipodi:role="line"
         x="107.43014"
         y="132.09383"
         style="font-size:0.00352781px;line-height:1.25;fill:#ffffff;stroke-width:0.26458332;"
         id="tspan3756">c </tspan><tspan
         sodipodi:role="line"
         x="107.43014"
         y="132.09824"
         style="font-size:0.00352781px;line-height:1.25;fill:#ffffff;stroke-width:0.26458332;"
         id="tspan3758">o </tspan><tspan
         sodipodi:role="line"
         x="107.43014"
         y="132.10265"
         style="font-size:0.00352781px;line-height:1.25;fill:#ffffff;stroke-width:0.26458332;"
         id="tspan3760">C </tspan><tspan
         sodipodi:role="line"
         x="107.43014"
         y="132.10706"
         style="font-size:0.00352781px;line-height:1.25;fill:#ffffff;stroke-width:0.26458332;"
         id="tspan3762">T </tspan><tspan
         sodipodi:role="line"
         x="107.43014"
         y="132.11147"
         style="font-size:0.00352781px;line-height:1.25;fill:#ffffff;stroke-width:0.26458332;"
         id="tspan3764">F { 3 n h 4 n </tspan><tspan
         sodipodi:role="line"
         x="107.43014"
         y="132.11588"
         style="font-size:0.00352781px;line-height:1.25;fill:#ffffff;stroke-width:0.26458332;"
         id="tspan3752">c 3 d _ 2 4 3 7 4 6 7 5 }</tspan></text>

# Big Zip (General skills, easy)
Unzip this archive and find the flag.
grep -r -o "picoCTF{.*}" big-zip-files
grep: Search tool for text patterns.
-r: Recursive search through all files in directories.
-o: Only output the matched portion, not the whole line.
"picoCTF{.*}": This is a regex pattern
Search every file under big-zip-files and extract all substrings that look like picoCTF flags.

# vault-door-training (Reverse Engineering, easy)
Your mission is to enter Dr. Evil's laboratory and retrieve the blueprints for his Doomsday Project. The laboratory is protected by a series of locked vault doors. Each door is controlled by a computer and requires a password to open. Unfortunately, our undercover agents have not been able to obtain the secret passwords for the vault doors, but one of our junior agents obtained the source code for each vault's computer! You will need to read the source code for each level to figure out what the password is for that vault door. As a warmup, we have created a replica vault in our training facility.

The source code for the training vault is here: VaultDoorTraining.java
Read the VaultDoorTraining.java to understand the password is picoCTF{w4rm1ng_Up_w1tH_jAv4_000AXPNPN0i}
Password is hardcoded in VaultDoorTraining.java.


# keygenme-py (Reverse Engineering, medium)
Read the code and find hashlib.sha256(bUsername_trial).hexdigest()[4]. Do for idx 4, 5, 3, 6, 2, 7, 1, 8.
Learning pt: hashlib.sha256(bUsername_trial) returns a SHA-256 hash object.
.digest() returns raw 32-Byte hash.
.hexdigest() returns 64-character hexadecimal string (1 Byte = 2 hexadecimal characters)

Add these code.
print(f"bUsername_trial: {bUsername_trial}")
print(f"{hashlib.sha256(bUsername_trial).hexdigest()}")
print(f"{key_part_static1_trial}{hashlib.sha256(bUsername_trial).hexdigest()[4]}{hashlib.sha256(bUsername_trial).hexdigest()[5]}{hashlib.sha256(bUsername_trial).hexdigest()[3]}{hashlib.sha256(bUsername_trial).hexdigest()[6]}{hashlib.sha256(bUsername_trial).hexdigest()[2]}{hashlib.sha256(bUsername_trial).hexdigest()[7]}{hashlib.sha256(bUsername_trial).hexdigest()[1]}{hashlib.sha256(bUsername_trial).hexdigest()[8]}{key_part_static2_trial}")

# buffer overflow 0 (Binary Exploitation, medium)
Let's start off simple, can you overflow the correct buffer? The program is available here. You can view source here.
char input[100];
char buf2[16];
strcpy(buf2, input);
writing 17 characters to input will cause technical overflow.
fgets(flag,FLAGSIZE_MAX,f); reads a line from file f (opened from flag.txt) and stores it into the global buffer flag.
signal(SIGSEGV, sigsegv_handler); This installs a signal handler for segmentation faults (SIGSEGV).
SIGSEGV = signal raised when the program does something illegal in memory, such as:
- invalid pointer dereference
- stack corruption (buffer overflow)
- accessing unmapped memory
If this program crashes due to a segmentation fault, don’t terminate immediately—run this function instead.
The function will print the flag.

19B will not trigger a segmentation fault. 20B will.
16 → safe (buf2)
17–19 → padding / harmless overwrite
20 → crosses into sensitive region → crash
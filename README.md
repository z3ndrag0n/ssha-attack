# ssha-attack
SSHA Attack

This simple prog is the first release of a tool to attack, or try to crack,
salted SHA hashes (SSHA) as they are used in some of today's modern day apps,
especially LDAP. RFC-3112 provides more details on this technology.  

This is not a silver bullet prog and simply works against a very specific type of data.
It DOES NOT crack every type of salted hash in existence.
Read the usage statement for more details, ./ssha_attack -h.

The prog currently supports dictionary style attacks as well as some brute-force models.

The OpenSSL lib's are required.

To compile untar and:

make clean
make

The prog should compile cleanly on any recent version of x-86 based Linux.
It was created on Fedora Core 5.

Before using the prog decide what attack model you want to follow.  
Your current choices are:

Dictionary based attack (-d)
Brute force incremental attack with a predefined alphabet (that you choose) (-a [1 - 10] and -n)
Brute force attack with a custom alphabet you provide (-a 20 and -c)
Brute force incremental attack with a custom alphabet you provide (-a 20 and -c and -n)

To run:

############### Dictionary attack ######################################
Dictionary based attack

./ssha_attack -m dictionary -d dictionary.txt -s {SSHA}1sx3RjtI6KLpqb3hHPDTKqIVBd9UukC3

############### Dictionary attack ######################################

############### Brute-Force incremental ################################
Brute force attack with a predefined alphabet (that you choose)

./ssha_attack -m brute-force -a 4 -n 3 -s {SSHA}Ig272xI9C9H4kvL8vHA6UcK57Y4ad97O

Here are some examples from when I was unit testing:


./ssha_attack -m brute-force -n 3 -a 9 -s {SSHA}EEiUTlF29/g8H6GlqVJT8JtGhmMkeU4S

Hash Algorithm Detected: SHA1


Trying Word Length: 3

There is a match on value "3ee"

Elapsed time in seconds for successful attack: 5



./ssha_attack -m brute-force -a 9 -n 3 -s Tt8H7clbL9y8ryN4/RLYrCEsKqbjJsWcPmKb4wOdZDJzYWx0

Hash Algorithm Detected: SHA256


Trying Word Length: 3
No hits for Word Length: 3

Trying Word Length: 4

There is a match on value "test"

Elapsed time in seconds for successful attack: 91



./ssha_attack -m brute-force -n 3 -a 9 -s {SSHA}PT8wnRusJxl3E7JnW6ufaFNiO6RWy6qH

Hash Algorithm Detected: SHA1


Trying Word Length: 3
No hits for Word Length: 3

Trying Word Length: 4
No hits for Word Length: 4

Trying Word Length: 5

There is a match on value "Yt35T"

Elapsed time in seconds for successful attack: 10796


############### Brute-Force incremental ################################

############### Custom Alphabet ########################################
Brute force attack with a custom alphabet you provide

./ssha_attack -m brute-force -a 20 -c custom -s {SSHA}iLWyP3dJamxdFc6sHLSJErt69+mb6en+

Here are some examples from when I was unit testing:


./ssha_attack -m brute-force -a 20 -c "#hlsas" -s {SSHA}NhLfEHbVFjgBswQEgmnQdMf7/WmrPayi

Hash Algorithm Detected: SHA1


No hits with identical values for the alphabet ...


There is a match on value "sl#ash"

Elapsed time in seconds for successful attack: 0



./ssha_attack -m brute-force -a 20 -c "#slsah" -s CtUnKbdMFKl4lX7/82QYX4aZXrENlR8gRhM0ViB504JzYWx0

Hash Algorithm Detected: SHA256


No hits with identical values for the alphabet ...


There is a match on value "sl#ash"

Elapsed time in seconds for successful attack: 0

############### Custom Alphabet ########################################

############### Brute Force incremental with Custom Alphabet ###########
Brute force incremental attack with a custom alphabet you provide

./ssha_attack -m brute-force -a 20 -c custom -n 2 -s {SSHA}owN4fkZDoCeXo4iw1fzqWe9u4/79vrfQ


Here is an example from when I was unit testing:

./ssha_attack -m brute-force -a 20 -c tse -n 2 -s {SSHA256}H0fvfbrcXAzg3uAYesE5babwQGbTsFdhphdJ1jaUEUxzYWx0

Hash Algorithm Detected: SHA256


Trying Word Length: 2
No hits for Word Length: 2

Trying Word Length: 3
No hits for Word Length: 3

Trying Word Length: 4
No hits for Word Length: 4

Trying Word Length: 5
No hits for Word Length: 5

Trying Word Length: 6
No hits for Word Length: 6

Trying Word Length: 7

There is a match on value "testees"

Elapsed time in seconds for successful attack: 0

############### Brute Force incremental with Custom Alphabet ###########

Some things to keep in mind when using this prog....

If you know the length of the clear text string you are attacking you may be best
suited using the "-a 20 -c your_dict" options. Just pass in a -c value of that size and
the brute force process will work away at the target string. It would obviously help if
you know the characters for a given clear text string, if you do then you should also
use this same option. If your custom alphabet contains non alpha numeric characters
then enclose them in double quotes.

If you arent sure of the number of characters in the target clear text string then
use the "-a 20 -c your_dict -n x" option where x is the minimum size of the attack string.
This will force an incremental brute force using the alphabet passed in via the -c
switch.

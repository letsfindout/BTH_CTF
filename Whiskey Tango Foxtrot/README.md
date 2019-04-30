
# Whiskey Tango Foxtrot (WEB) - writeup **NOT COMPLETED YET**

## Challenge description
"I let you run eval in this one. Don't tell anyone."

## Given information
We are given two pieces of information. One is a picture of a PHP-code segment and the other one is a address and a portnumber where we face the code segment. 

![alt text](src.png "src")
  
## HOWTO
### Step 1. Analysing the code
So if we take a close look at the picture we see that there are two sections that has been censured. One is what **`$a`** has been assigned to and the other one seems to be the flag. We also see that we have a input using STDIN with fgets and that our input needs to match what's inside **`$a`**. Whatever we write does also need to match the regex of **`/^[\.\*a-zA-Z\d]+$/`** - which can be simply translated to *a string of minimum length one that only contain any of the following characters dot, asterix, a to z, A to Z or digits.* One thing we may not disregard as something that we can abuse is the **eval**-function. Since it evaluates something as PHP-code. If it were not for the **preg_match** we could simply enter **`$a`** and we would have found the flag. So we need to think about how PHP process the dot and asterix since they will be the key to make the **eval**-function recognize that what we wrote was a string. There is also the fact that if we write something that matches the **preg_match**, we will get a **vardump** of both our input and the correct input. 

### Step 2. Analysing the output
So lets just start of by entering something that will match with the **preg_match** so that we can se what the correct input should be. I chose to write `hello` and got the respons

hello <br/>
Strings(13) "192.260.370.1" <br/>
Strings(5) "hello" <br/>

So we are supposed to find a way to write a string without ", ' and so on which contain 192.260.370.1. Since **eval** evaluates a string as a PHP-code we know that it cannot recognize an IP-address since there is no formal datatype for it. But we do know that it recognize the primal datatypes, e.g int, float and so on. We know that float contains of dots,



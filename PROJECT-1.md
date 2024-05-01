## Project 1: Socket Basics

- This assignment is intended to familiarize you with writing simple network code. You will implement a client program that plays a variant of the recently-popular game Wordle. Your program will make guesses for the secret word, and the server will give you information about how close your guess is. Once your client correctly guesses the word, the server will return a secret flag that is unique for each student. If you receive the secret flag, then you know that your program has run successfully.
- Your client must support TLS encrypted sockets. The server will return different secret flags depending on whether your client communicates with or without TLS. To receive full credit on this project, you must turn in **both** secret flags: the one retrieved via a non-encrypted socket, and the one retrieved via a TLS encrypted socket.
- More information can be found here: https://3700.network/docs/projects/socketbasics/

### Approach:
My approach for this project was to first test connecting to the socket
and manually sending/receiving data. Once I was able to send/receive data with inputs
and outputs that matched the assignment specification, I then wrapped the socket
with a TLS socket to handle SSL. I then tested the TLS socket by sending/receiving data.
Once I got this working, I then implemented my strategy which is described below. Finally,
I created the argument parser to handle the arguments from the command line. I also handled
the safety of my program by catching exceptions when attempting to connect to the socket and
send/receive data from it.

### Challenges
The biggest challenge for me was sending and receiving data. Having to parse the JSON from strings
to objects and vice versa was difficult for me, and I ran into a few errors that took a decent
amount of time to resolve. I also had some difficulties receiving the data for every new line, and
I had to eventually use a while loop to receive the data until the server closed the connection.
The design of my program was also a bit challenging, as I wasn't sure if I wanted a class-based approach
or not but ultimately chose to do so to avoid using global variables.

### Strategy
My strategy for guessing words is as follows: I first start with what many researchers consider
the "best" starting word for wordle, which is "slate". I then filter the wordlist based on the
marks received from the initial guess. When the initial guess "slate" is sent to the server, I parse the
marks that are received and filter the wordlist accordingly. If the mark is a 2, I remove all words
that do not contain the same letter in the same position. If the mark is a 1, I remove all words that
contain the same letter in the same position. This makes for an efficient strategy that guesses in under 8
attempts, depending on the word.

### Testing
I first printed out the data that I received from the server to make sure that guesses were actually being
sent and received. I then tested my wordlist filtering function by printing the wordlist every time after it
was updated to make sure that my algorithm was updating the wordlist correctly. I then tested the TLS socket
by printing the data that was received from the server. I also used various command arguments that could be invalid,
such as an invalid port number, an invalid username, an invalid hostname, and even disabled my internet to ensure
my try-except blocks were handling all possible errors properly.

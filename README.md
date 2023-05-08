Download Link: https://assignmentchef.com/product/solved-seng265-c-assignment1
<br>
For this assignment, please ensure your work compiles and executes correctly on the Linux machines in ELW B238. You are welcome to use your own laptops and desktops for much of your programming; if you do this, give yourself a few days before the due date to iron out any bugs in the C program you have uploaded to the BSEng machines. (Bugs in this kind of programming tend to be platform specific, and something that works perfectly at home may end up crashing on a different hardware configuration.)

Objectives of this assignment

<ul>

 <li>Use the C programming language to write the first implementation of a file encoder (and decoder) named “RLE.c”</li>

 <li>Test your code against the provided test data, and other test data you create, to ensure it’s working as expected. The instructor will also be testing your program against test data that isn’t provided to you, so be sure to think creatively about how to “break” and strengthen your code!</li>

</ul>

<h1>This assignment: “RLE.c”</h1>

Bioinformatics is the management and use of biological information, particularly genetic information. It involves the application of computer sciences in order to solve problems in molecular biology. Biologists have become reliant on having access to shared data and analytical tools to do their research, but there are certain challenges, including the exponential growth of data. When performing experiments, scientists are often forced to rely on massive data warehouses and are looking for ways to transfer huge amounts of data as quickly as they can.​ There are numerous ways to improve this process, but one ubiquitous technique is to decrease the amount of data needing to be transferred using compression methods.

In Bioinformatics, one example of data is DNA sequences (e.g. sequences made from the letters A, C, G, and T, representing the nucleobases Adenine, Cytosine, Guanine and Thymine, the molecular building blocks of all DNA).

Source: genome.gov

An example of such a sequence would be:

AACCCTAAAATTGGAA

In this assignment, we will use Run-Length Encoding as a lossless data compression technique to condense the repetitive parts of DNA sequences. RLE might not be a biologist’s first choice for which compression technique to select and apply, but it will give us an entry point to discuss compression algorithms and their implementation.

In particular, we are interested in both the encoding of sequences (translating the original format into an encoded format), and the inverse decoding operation, which translates the encoded format back into the original sequences.

<h1>Encoding</h1>

To store the original example sequence “AACCCTAAAATTGGAA” in memory would require one byte per character, or 16 bytes in total

To start RLE, we start with the first character, which in this example is ‘A’. Then we look at the second character, which is ‘A’. Then we evaluate whether the first character is the same as the second character. In this case, it is. Since the last two characters were both the same, we’re now going to look at the third character and see if it is also the same. The third character is ‘C’, so we have found the end of the streak of ‘A’s. Since we have reached the end of the streak of ‘A’s, we now write out the character in the streak and number of times it occurs in the streak.

Output: ​<strong>A2 </strong>

The third character ‘C’ in this example is the beginning of a streak of three characters. So we add this to the output: Output: A2​<strong>C3 </strong>

The first character that appears after the streak of ‘C’s is a T.  Only one T appears at that point so the out is now changed to:

Output: A2C3<strong>T1</strong>​

We continue this process until we reach the end of the sequence, and can produce the final encoded output:

<strong>Final Encoded Output : A2C3T1A4T2G2A2 </strong>

The length of the output is 14 bytes. This is 2 bytes less than the 16 bytes for the original sequence.

<h1>Decoding</h1>

To decode the encoded sequences, we need to iterate through the characters in the encoded string as “sub-sequences”.  Each sub-sequence is a letter followed by a one-digit number. The first character is the original letter, and the next character is the number of consecutive instances of that letter in the original sequence. So, returning to the output from the encoding example, let’s run it through the decoding process.

The encoded string is: ​<strong>A2C3T1A4T2G2A2. </strong>

The ​<em>first </em>​character is ‘A’ and the count is 2. So we build a new output string: Decoded Output : ​<strong>AA </strong>

The ​<em>third </em>​character is ‘C’ and the count is 3.

Decoded Output : AA​<strong>CCC </strong>

The ​<em>fifth </em>​character is ‘T’ and the count 1.

Decoded Output : AACCC​<strong>T </strong>

From observing the positions of the letters in the encoded format, We can deduce that each odd-numbered character (starting from 1) in the string to be decoded is an encoded letter, and each even-numbered character is the count of the number of occurrences of that letter in the original sequence.

The seventh character is ‘A’ and the count 4.

Decoded Output : AACCCT​<strong>AAAA </strong>

The ninth character is ‘T’ and the count 2.

Decoded Output : AACCCTAAAA​<strong>TT </strong>

The eleventh character is ‘G’ and the count 2.

Decoded Output : AACCCTAAAATT​<strong>GG </strong>

The thirteenth character is ‘A’ and the count 2.

Decoded Output : AACCCTAAAATTGG​<strong>AA </strong>

<strong>Final Decoded Output : AACCCTAAAATTGGAA</strong>

<h1>Requirements</h1>

The requirements for this assignment are as follows:

<ol>

 <li>Use arrays (and not dynamic memory allocation!) as an aggregate data type for file processing (encoding and decoding).</li>

 <li>Create a <strong>main ​</strong>​ function that:

  <ol>

   <li>Takes two command line arguments:

    <ol>

     <li>A string indicating the name of the file to operate on;</li>

     <li>A​ one-character flag indicating whether the program should operate in encoding or decoding mode. Use ‘e’ for encoding mode, or ‘d’ for decoding mode.</li>

    </ol></li>

  </ol></li>

</ol>

<ul>

 <li>If the second argument is not provided, or is not either ‘e’ or ‘d’,

  <ol>

   <li>print “Invalid Usage, expected: RLE {filename} [e | d]” to the console</li>

   <li>terminate the program with exit code 4.</li>

  </ol></li>

</ul>

<ol>

 <li>Opens the file indicated by the first argument.

  <ol>

   <li>If there is no filename specified:

    <ol>

     <li>print “Error: No input file specified!” to the console 2. terminate the program with exit code 1. ii. If the filename specified doesn’t exist or can’t be read for any reason:</li>

     <li>print “Read error: file not found or cannot be read” to ​the console 2. terminate the program with exit code 2.</li>

    </ol></li>

   <li>Reads one line from e file into a C string. The single line will be a maximum of 40 characters (we will process only the first line, there should be no new line character as input, or subsequent line processing). The encoded and decoded file formats should follow these rules:

    <ol>

     <li>Each file must only contain upper case letters, digits and optional whitespace.</li>

     <li>If the file contains any whitespace characters, they must be at the end of the file, and must be ignored.</li>

    </ol></li>

  </ol></li>

</ol>

<ul>

 <li>If within the given file any non-whitespace character follows any whitespace character, or any non-whitespace character other than a digit or an upper-case letter, the file should be considered to be in an invalid format. Upon detecting this situation, the program should: 1. print “Error: Invalid format” to the console 2. terminate the program with exit code 3.</li>

</ul>

<ol>

 <li>Depending on the value of the second command-line argument, passes the string read from the input file to the <strong>encode ​</strong>​ or <strong>decode ​</strong>​          function as described below.</li>

</ol>




<ol start="3">

 <li>Create a second function called <strong>encode ​</strong>​ with the following characteristics:

  <ol>

   <li>Take a C string as a function parameter.</li>

   <li>Encode the provided string using the algorithm described above – to simplify, the sequences in this assignment will be limited to the range of [2-9] in length</li>

   <li>If the string was encoded successfully:

    <ol>

     <li>print the resulting encoded representation to the console</li>

     <li>terminate the program with exit code 0, indicating success</li>

    </ol></li>

   <li>If the string could not be encoded for any reason (e.g. badly formatted):

    <ol>

     <li>print “Error: String could not be encoded” to the console ii. terminate the program with exit code 5</li>

    </ol></li>

  </ol></li>

</ol>




<ol start="4">

 <li>Create a third function called <strong>decode ​</strong>​ with the following characteristics:

  <ol>

   <li>Take a C string as a function parameter</li>

   <li>Decode the provided string using the algorithm described above</li>

   <li>If the string was decoded successfully:

    <ol>

     <li>print the resulting decoded representation to the console</li>

     <li>terminate the program with exit code 0, indicating success</li>

    </ol></li>

   <li>If the string could not be decoded for any reason (e.g. badly formatted):

    <ol>

     <li>print “Error: String could not be decoded” to the console terminate the program with exit code 5</li>

    </ol></li>

  </ol></li>

</ol>

<h1>Provided Materials</h1>

We have created a git repository for you containing a test suite and these instructions.

Test Suite

We will supply a suite of test cases that you can use to evaluate your own program, and get a feel for the types of inputs you can expect.

The test suite is structured as a set of directories, one per test case. Each test case directory will have the following characteristics: – The directory is named according to the type of test, e.g. <strong>encode_badInput_letterAfterWhitespace</strong>

<ul>

 <li>The first word in the directory name will be <strong>encode​</strong>​ or <strong>decode​</strong>​          , indicating which mode your program should be in when running this test case.</li>

 <li>Any additional text in the directory name (e.g. <strong>_badInput_letterAfterWhitespace</strong>​ in this example) is informational and can be ignored.</li>

 <li>The directory always contains a single file named <strong>txt​</strong>​ that your program is expected to read as its input</li>

 <li>If your program is expected to run successfully given this input, the directory will contain a file named <strong>txt​</strong>​ that your program’s output is expected to precisely match</li>

 <li>If your program is expected to terminate with a non-zero (unsuccessful) error code when given this input, the directory will contain one of the following:</li>

 <li>a file named <strong><em>​</em></strong>​ <strong>err.txt​</strong>, where n is the expected exit code, containing text that your program’s output is expected to precisely match,​<strong> or; </strong></li>

 <li>a file named <strong><em>​</em></strong>​ <strong>err​</strong>, where n is the expected exit code. In this case your output doesn’t need to match any specific error message.</li>

</ul>

<h1>Process</h1>

To get started, the assignment repository has already been set up in your person GitLab space, listed as /assignment1.git. We set this up in our local machine space with <strong>git clone​</strong>​   :

(all one line, with &lt;NETLINK_ID&gt; replaced with your personal Netlink identifier)

Note that by cloning from your personal repository, this automatically sets up your remote on GitLab so when you <strong>git push​</strong>​         later, your changes will automatically be visible to both you and the teaching team.

Use a text editor to write your program.

Once you’re able to compile your program, test it by running it with the <strong>input.txt​</strong>​      files in the provided test suite, and any other files you can think of. Be creative; try to predict what kinds of inputs will break your code! Try random files lying around on your computer or the internet to see what happens!

If it seems like your changes are having no effect, don’t forget to recompile your program after changing it!

When you’ve made changes to the file that you want to keep, <strong>git commit ​</strong>​    your changes to your local copy of the repository. Git will save the history of past commits. When you want to upload your changes to your repository, use <strong>git push​</strong>​              .

<h1>Deliverables</h1>

<ul>

 <li>Write a C program in a file named RLE.c (case sensitive), <u>​</u><u>placed in the root of your</u> <u>repository</u>​, that implements the above requirements.</li>

 <li>The program must compile successfully using <strong>gcc​</strong>​ .</li>

 <li>The assignment will be marked based on the last version of your program pushed before the deadline.</li>

</ul>
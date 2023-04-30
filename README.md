Download Link: https://assignmentchef.com/product/solved-final-project-secure-hash-algorithm-sha-1
<br>
Your final project is to implement the Secure Hash Algorithm (SHA-1) in C or C++.

<ul>

 <li>This algorithm <strong>takes a file</strong>, cuts up and mixes the data, and <strong>produces a hash value</strong>, which is <strong>a number</strong>in a specific range.</li>

 <li>The <strong>hash value for SHA1 is 160 bits long</strong>, so it has a decimal value of 2<sup>160</sup>, which is roughly the number of atoms on planet Earth.</li>

 <li>The SHA-1 hash value is often used in data security for such things as storing passwords securely, error detection, comparing files, and digital signatures.

  <ul>

   <li>Today, many applications still rely on SHA-1, even though theoretical attacks have been known since 2005, and SHA-1 was officially deprecated by NIST in 2011. For more on this see:<a href="https://shattered.io/">https://shattered.io/</a></li>

   <li>The attack proving SHA-1 vulnerability required over 9,223,372,036,854,775,808 SHA1 computations. This took the equivalent processing power as 6,500 years of single-CPU computations and 110 years of single-GPU computations.</li>

  </ul></li>

 <li>For detailed specifications of the algorithm, see the NIST document<strong><em>FIPS180-1-SecureHashStandard.pdf</em></strong>attached below.

  <ul>

   <li>The specifications are “a bit technical”, but <strong><em>you should spend some time reading it before attempting the project!</em></strong></li>

   <li>The description of the algorithm begins on page 6.</li>

   <li>Appendices A-C have very detailed output that you can use to debug your program. Make sure you understand the document well enough to grasp what Appendix A is saying about the output.</li>

   <li>The 3 input files described in the appendices are attached below.

    <ul>

     <li>Appendix A input file is: abc.txt</li>

     <li>Appendix B input file is: alpha.txt</li>

     <li>Appendix C input file is: a.txt</li>

    </ul></li>

   <li>In the document, “word” refers to data type “int”, both which are 32 bits.</li>

  </ul></li>

</ul>

<strong>Development and Testing Procedure:</strong>

<ul>

 <li>Write your program using the document specifications and the instructions below.</li>

 <li>Make “debug” print statements so that it will print output like that shown Appendix A.

  <ul>

   <li>I suggest you make a global int to use as a boolean to turn debug printing on and off in all functions.</li>

  </ul></li>

 <li><strong>TEST each function as you are writing them! </strong><strong>DO NOT attempt to write a big chunk of this thing before you test</strong><strong>, it will be impossible to debug!</strong></li>

</ul>

<ol>

 <li>Use abc.txt and Appendix A to write your functions. This is the shortest input file. It has only one “block” as described in the specifications. You should get your output to match all steps shown in Appendix A before moving to the next larger file alpha.txt.</li>

 <li>Test alpha.txt and get your output to match all steps shown in Appendix B.</li>

 <li>Before attempting to hash the largest file a.txt,  <strong>TURN OFF PRINTING </strong>for everything except the final “message digest” outcome! The output will be massive otherwise.</li>

</ol>

<ul>

 <li>Wikipedia also has example hashes and SHA-1 pseudocode at <a href="https://en.wikipedia.org/wiki/SHA-1">http://en.wikipedia.org/wiki/SHA-1</a></li>

 <li><strong><em>The “message digest” is the SHA-1 hash that should be the final program output.</em></strong></li>

</ul>

<strong> </strong>

<strong>Instructions for required functions:</strong>

<strong>Instructions for readFile function:</strong>

<strong>unsigned int readFile(unsigned char buffer[])</strong>

<ul>

 <li>The entire contents of the file will be read into and stored in the <strong>buffer[]</strong>array

  <ul>

   <li>A 1 (one) bit is appended to the end of the <strong>buffer[]</strong>array</li>

   <li>The function returns the number of characters in the file (size of file in<strong>bytes)</strong>. You need this!</li>

   <li>This is similar to the character counting program from Session 7: counting.c</li>

  </ul></li>

 <li>Input and count the characters from standard input (stdin) until the end-of-file (EOF).

  <ul>

   <li>For file input, create a text file or use the provided .txt files below, use the stdin redirection operator (&lt;) on the commandline .</li>

  </ul></li>

 <li>The buffer array will store the characters. It will be a large array of UNSIGNED (not signed) characters.

  <ul>

   <li>The largest input file to test your program is 1 million characters, but set your array MAX_SIZE to 1048576 (1 megabyte), or larger.

    <ul>

     <li><strong><em>Warning</em></strong><strong>: </strong>Your program might not get the correct result for 1 million a’s file (a.txt), if you use 1000001 as the max.</li>

    </ul></li>

   <li>Make sure that you have error checking to stop the program and tell the user when the input file is too big for your program.</li>

  </ul></li>

 <li>At this point you should check if your program puts the correct characters into your array, and counts the correct number of bytes in the file.</li>

 <li>This also might be a good place to append the 1 (one) bit at the end of the message.

  <ul>

   <li><strong><em>Note </em></strong>that this is equivalent to adding the byte 0x80 after the last character in the buffer array.</li>

   <li>For the abc.txt example: buffer[0] = ‘a’ = 0x61, buffer[1] = ‘b’ = 0x62, buffer[2] = ‘c’ = 0x63, and buffer[3] = 0x80.</li>

  </ul></li>

</ul>

<strong> Instructions for calculateBlocks function:</strong>

<strong>unsigned int calculateBlocks(unsigned int sizeOfFileInBytes)</strong>

<ul>

 <li>The next step is to calculate the block count.

  <ul>

   <li>Since each block is 512 bits, divide the total bits (<strong><em>not bytes</em></strong>) in the file by 512.</li>

   <li>Before dividing by 512,  make sure to add 1 (one) to the total count to account for the 1 (one) bit that is appended to the end of the data from the file.</li>

  </ul></li>

 <li>Since the last 64 bits at the end of the last block are reserved for the bit count (not byte count) of the file, one more block must be added for any message that has a final block that is greater than 448 (512 – 64) bits.</li>

</ul>




<ul>

 <li>This equation will calculate the block count:</li>

</ul>

(((8 * sizeOfFileInBytes) + 1) / 512) + 1

<ul>

 <li>This <strong>if </strong>statement will determine if an extra block needs to be added or not:</li>

</ul>

if((((8 * sizeOfFileInBytes) + 1) % 512) &gt; (512 – 64))blockCount = blockCount + 1




<ul>

 <li>For the abc.txt example:

  <ul>

   <li>blocks = ((((8 * sizeOfFileInBytes) + 1) / 512) + 1) = ((((8 * 3) + 1) / 512) + 1) = (0 + 1) = 1.</li>

   <li>There is no extra block, because the statement if((((8 * sizeOfFileInBytes) + 1) % 512) &gt; (512 – 64)) = if((((8 * 3) + 1) % 512) &gt; (512 – 64)) = if(25 &gt; 448) is false.</li>

  </ul></li>

</ul>

<strong>Instructions for convertCharArrayToIntArray</strong><strong> </strong><strong>function:</strong>

<strong>void convertCharArrayToIntArray(unsigned char buffer[], unsigned int message[], unsigned int sizeOfFileInBytes)</strong>

<ul>

 <li>It is easier to read from a file using an array of unsigned characters (buffer[]), but it is easier to process each block (512 bits or 16 integers) using an array of unsigned integers (here named message[])

  <ul>

   <li>You should convert your array of unsigned characters into an equivalent array of unsigned integers.</li>

   <li>We did this in the assignment on C Bitwise Operators, where we packed 4 characters into 1 integer variable.</li>

  </ul></li>

</ul>

<strong>Instructions for addBitCountToLastBlock function:</strong>

<strong>void addBitCountToLastBlock(unsigned int message[], unsigned int sizeOfFileInBytes, unsigned int blockCount)</strong>

<ul>

 <li>You need to insert the size of the file in bits into the last index of the last block.</li>

</ul>

<ol>

 <li>Calculate the index of last word (integer) in the message[] array.

  <ul>

   <li>In the document, “word” refers to data type “int”, both which are 32 bits.</li>

  </ul></li>

 <li>Insert the number of bits in the file to the last integer (word) of the message[] array.

  <ul>

   <li>There are 8 bits in a byte, so sizeOfTheFileInBits = sizeOfFileInBytes * 8</li>

   <li>There are 16 integer array elements in each block, so indexOfEndOfLastBlock = (blockCount * 16) – 1.</li>

  </ul></li>

</ol>

<strong>Instructions for computeMessageDigest function:</strong>

<strong>void computeMessageDigest(unsigned int message[], unsigned int blockCount)</strong>

<ul>

 <li>The final step is to compute the message digest, which is described in the document in parts 5, 6, and 7 (pages 9-12).</li>

</ul>

<ol>

 <li>Initialize variables as described in the document on page 11.

  <ul>

   <li>H0 = 0x67452301</li>

   <li>H1 = 0xEFCDAB89</li>

   <li>..</li>

  </ul></li>

 <li>Loop through each block, and complete steps a, b, c, d, and e as described in the document.</li>

</ol>

<strong> </strong>

<strong>Instructions for helper functions f and K</strong>

<strong>unsigned int f(unsigned int t, unsigned int B, unsigned int C, unsigned int D)</strong>.

<strong>unsigned int K(unsigned int t)</strong>




These will return the values described in Part 5 (function f<sub>t</sub>(B,C,D)) and Part 6 (constants K<sub>t</sub>)

<ul>

 <li>note that the C/C++ code “if(0 &lt;= t &amp;&amp; t &lt;=19)” is equivalent to the the pseudocode statement “if(0 &lt;= t &lt;=19)”.</li>

 <li>Equivalent C/C++ notation to document:</li>

</ul>

C/C++ operator: &amp;  is equivalent to X AND Y = X &amp; Y = bitwise “and” of X and YC/C++ operator: | is equivalent to  X OR Y = X | Y = bitwise “inclusive-or” of X and YC/C++ operator: ^ is equivalent to X XOR Y = X ^ Y = bitwise “exclusive-or” of X and YC/C++ operator: ~ is equivalent to NOT X = ~X = bitwise “complement” of XC/C++ operator: + is equivalent to X + Y = 2<sup>32</sup> modulus addition



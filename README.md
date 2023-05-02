Download Link: https://assignmentchef.com/product/solved-comp206-assignment6
<br>
<strong>Ex. 1 —                     A Polynomail Evaluation App</strong>

In this exercise, you will create a C modules based program, polyapp to implement a simple application that constructs a polynomial expression and evaluates it for certain predetermined values.

The polyapp application will receive a text file as input, that contains multiple lines of data to construct a polynomial. Each line will contain the <em>coefficient </em>and <em>exponent </em>of a term in the polynomial. For example, below is an example file that represents the polynomial 12<em>x</em><sup>3</sup>− 4<em>x</em><sup>5</sup>.

<table width="681">

 <tbody>

  <tr>

   <td width="681">$ cat data.ssv</td>

  </tr>

  <tr>

   <td width="681"></td>

  </tr>

 </tbody>

</table>

Here 12 and 3 are the coefficient and exponent of the term 12<em>x</em><sup>3</sup>, respectively, and so forth. You can use vi to create a data files of your own for testing purposes.

1.Create a directory for this assignment and initialize with git (just a local repository, do not make it public). As you progress through this assignment, you will keep commiting code to git (I leave the actual points in development where you feel like you should commit the code to git up to you, but <strong>there should be at least 4 commits separated out by 15 minutes or more</strong>).

2.All your program files should include a comment section at the beginning that describes its purpose (couple of lines), the author (your name), your department, a small “history” section indicating what changes you did on what date. The code should be properly indented for readability as well as contain any additional comments required to understand the program logic.

3.Your main will be in a C file polyapp.c. Your program will be invoked as follows by passing a data file as its argument. (Therefore, do not assume the name of the data file, but read it from the argument).

$ ./polyapp polydata.csv

Although mini tester will not do any negative test cases by invoking the program with no file names as argument etc., I highly encourage you to include such logic in your program so that it is easy for you to develop and debug your program.

4.In your main, use fgets to read one line at a time from the data file.

5.Use vi to create a C file, utils.c.

Create a function parse that accepts a string, and two integer pointers as its argument. Your main will use this parse function to parse a line that was retrieved using fgets and store the coefficient and exponent to the address provided in the integer pointers.

Create a function powi that accepts two integers as argument (x and exponent) it returns an integer which is x raised to the power of exponent. For example, if it is passed 2 and 3, it will return 8, which is 2<sup>3</sup>. You <strong>must not use </strong>math.h to perform this. Write your own simple loop to do the computation.

6.Create a C file poly.c. Here you will make a linked list that can be used to store a polynomial of arbitrary length. Your linked list must use the following structure for its nodes.

<strong>struct </strong>PolyTerm

{

<strong>int </strong>coeff ; <strong>int </strong>expo ;

<strong>struct </strong>PolyTerm ∗next ;

};

You will need a global variable, head, in this C file to keep track of the polynomial linked list. This C file will need a minimum of the following three functions (you are recommended to have more, as needed, to make your program modular and easy to develop and debug).

addPolyTerm is a function that accepts two integer arguments (a coefficient and exponent) and assimilates that term into the existing Polynomial. It returns an integer as its return value. A 0 return indicates success and a -1 for failure (as in for example, ran out of memory, so could not add a new node to the polynomial linked list). displayPolynomial is a function that accepts no arguments and has no return. It will display the polynomial expression (will see the format later).

evaluatePolynomial is a function that accepts an integer value for x and returns an integer that is obtained by evaluating the polynomial. This function will have to traverse the linked list, getting the values for coefficient and exponent from each node and using the powi function to perform computations.

7.Have your main parse each line of the data file to extract the coefficient and exponent and add it to the polynomial using the addPolyTerm function. If you run out of memory (the tester has no test cases for this), print an appropriate message and terminate your program from the main.

8.When all the polynomial terms are read and the polynomial is fully constructed, the main should call displayPolynomial to print the polynomial expression to the screen (format will be specified below).

9.Next, the main should call evaluatePolynomial for the values (-2, -1, 0, 1, -2) in that order and print the results (format will be specified below).

10.You may need additional header files (.h) to make sure your various C files can interact with each other. Create them as necessary and include them in appropriate files as needed. The objective is that make / gcc should not give any compilation warnings and errors.

11.Create a make file, name it Makefile . This make file should contain necessary compilation steps to build your final executable, which should be named polyapp. Your program should build an executable if TAs download your source code into an empty directory and just typed make . Therefore, make sure whatever commands you include in your make file is not your custom scripts, aliases, etc., but regular commands available to everyone in mimi.

<h1>Point distribution</h1>

1.For writing comments on all of your files.

2.<strong> </strong>Turn in your git log, by redirecting its output and store it to a file gitlog.txt. It should show <strong>at least 4 commits which are separated by at least 15 minutes or more</strong>.

3.For compiling properly with the make command. The make file should be written in such a way that it compiles only the files that are “changed” and files that are dependant on that changed file (and so forth).

4.<strong> </strong>Proper use of header files to provide as well as limit the exposure of functions and variables to other C files.

5.<strong> </strong>For displaying the polynomial. The polynomial should be printed in the increasing order of the exponents. You can incorporate the logic to store the terms in sorted order in the linked list as and when you are adding each term into the polynomial linked list.

<table width="651">

 <tbody>

  <tr>

   <td width="651">$ cat data1.ssv12 33    04    5$ ./polyapp data1.ssv0x2+12×3+4×5 for x=-2, y=-224 for x=-1, y=-16 for x=0, y=0 for x=1, y=16 for x=2, y=224</td>

  </tr>

 </tbody>

</table>

6.<strong> </strong>For merging polynomial terms with the same exponent. You will have to incorporate this logic when you are adding each term into the polynomial linked list one-by-one. (You may still display polynomial terms whose coefficient evaluates to 0 as such and is not necessary to remove them).

<table width="651">

 <tbody>

  <tr>

   <td width="651">$ cat data2.ssv12 3 3 0-4 24 53 2$ ./polyapp data2.ssv 3×0-1×2+12×3+4×5 for x=-2, y=-225 for x=-1, y=-14 for x=0, y=3 for x=1, y=18 for x=2, y=223</td>

  </tr>

 </tbody>

</table>

7.<strong> </strong>For correct evaluation of polynomial expression for different values.

All coefficients will be whole number integers (-negative through zero to positive). All exponents will be whole numbers (zero through positive integers).
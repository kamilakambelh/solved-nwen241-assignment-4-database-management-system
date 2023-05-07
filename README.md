Download Link: https://assignmentchef.com/product/solved-nwen241-assignment-4-database-management-system
<br>
In the previous assignment, you implemented a database table using a dynamically allocated array (of structures) for holding records in memory. In this assignment, you will use vector and linked list to implement the same database table. You will also use File input/output operations to retrieve the table from a comma-separated value (CSV) file.

<strong>Program Design</strong>

(This is already partly discussed in Assignment #3.)

A fundamental concept in DBMS is the <em>table</em>. A table consists of zero or more <em>records </em>or entries, and each record can have one or more <em>fields </em>or columns. An example of a table for storing information about movies is shown below:

<table width="542">

 <tbody>

  <tr>

   <td width="30">id</td>

   <td width="311">title</td>

   <td width="45">year</td>

   <td width="155">director</td>

  </tr>

  <tr>

   <td width="30">13</td>

   <td width="311">The Shawshank Redemption</td>

   <td width="45">1994</td>

   <td width="155">Frank Darabont</td>

  </tr>

  <tr>

   <td width="30">25</td>

   <td width="311">The Godfather</td>

   <td width="45">1972</td>

   <td width="155">Francis Ford Coppola</td>

  </tr>

  <tr>

   <td width="30">31</td>

   <td width="311">The Dark Knight</td>

   <td width="45">2008</td>

   <td width="155">Christopher Nolan</td>

  </tr>

  <tr>

   <td width="30">40</td>

   <td width="311">The Godfather: Part II</td>

   <td width="45">1974</td>

   <td width="155">Francis Ford Coppola</td>

  </tr>

  <tr>

   <td width="30">55</td>

   <td width="311">The Lord of the Rings: The Return of the King</td>

   <td width="45">2003</td>

   <td width="155">Peter Jackson</td>

  </tr>

  <tr>

   <td width="30">72</td>

   <td width="311">Pulp Fiction</td>

   <td width="45">1994</td>

   <td width="155">Quentin Tarantino</td>

  </tr>

 </tbody>

</table>

This table contains 6 rows or records. Each record has 4 fields, namely, id, title, year, and director.

<strong>In this assignment, you will focus on implementing a single database table with 4 fields (id, title, year, and director). </strong>A C structure with tag movie will be used for holding a table record. The structure declaration is given below and is defined within dbms2 namespace in dbms2.hh:

namespace dbms2 { <strong>struct </strong>movie { <strong>unsigned long </strong>id; <strong>char </strong>title[50]; <strong>unsigned short </strong>year; <strong>char </strong>director[50];

}; }

<strong>Task 1.</strong>

Basics

In this task, you will declare a C++ abstract class for representing a database table. The class should be named AbstractDbTable and should have the following public members:

<ul>

 <li>A function namedmodify any member variables.rows() which returns an integer, and should notThis should be declared as a pure virtual function. <em>In the implementation</em>, the function should return the number of rows in the table.</li>

 <li>A function named<sub>should not modify any member variables. This should be declared as</sub>show() which accepts an integer parameter, and a pure virtual function. <em>In the implementation</em>, the function should display the information stored in a row. You are free to format the print out, but all fields of the row should be shown. The input parameter indicates the row number of the record to be displayed. If the record exists, the function should return true, otherwise, it should return false.</li>

 <li>A function namedture. This should be declared as a pure virtual function.add() which accepts a reference to a movie<em><sub>In the imple-</sub></em>struc<em>mentation</em>, the function should insert a record into the table. The input parameter contains the record details to be stored in the table. The function should return true if the record was successfully inserted into the table, otherwise, it should return false.</li>

 <li>A function namedger. This should be declared as a pure virtual function.remove() which accepts an unsigned long inte-<em>In the implementation</em>, the function should remove a record from the table. The input parameter contains the id of the record to be removed. The function should return true if the removal was successful, otherwise, it should return false.</li>

 <li>A function named<sub>should not modify any member variables. This should be declared</sub>get() which accepts an integer parameter and as a pure virtual function. <em>In the implementation</em>, the function should return a pointer to a movie structure. The input parameter indicates the row number of the record to be returned.</li>

 <li>bool loadCSV(const char<sub>a normal (non-virtual) function. See Task 5 for more details.</sub>*infn): This should be declared as</li>

 <li>bool saveCSV(const char<sub>as a normal (non-virtual) function. See Task 6 for more details.</sub>*outfn): This should be declared</li>

</ul>

Note that you have implemented the first four functions in Assignment #3 for a database table implemented as an array of structures. In this assignment, you will implement them for a database table that uses a vector (Task 4) and a linked list (Task 7).

The class should be defined within dbms2 namespace. Save the class in a header file named dbms2.hh.

<strong>Task 2.</strong>

Basics [

Declare a C++ class named VectorDbTable that is a subclass of AbstractDbTable. You will use this class to implement a database table using a vector. You may declare constructors, destructors, additional member variables and functions. Provide sufficient comments to justify the declaration of these additional members.

The class should be defined within dbms2 namespace. Save the class in a header file named vdb.hh.

<strong>Task 3.</strong>

Basics

Declare a C++ class named LinkedListDbTable that is a subclass of AbstractDbTable. You will use this class to implement a database table using a linked list data structure. You may declare constructors, destructors, additional member variables and functions. Provide sufficient comments to justify the declaration of these additional members.

The class should be defined within dbms2 namespace. Save the class in a header file named lldb.hh.

<strong>Task 4.</strong>

Completion

Provide an implementation of the class VectorDbTable as declared in vdb.hh.

Save the implementation in vdb.cc.

(Hint: Implementing a class means implementing all unimplemented member functions, constructors and destructors declared in the class declaration.)

<strong>Task 5.</strong>

Completion

Provide an implementation of the member function

bool loadCSV(<strong>const char </strong>*infn)

in the AbstractDbTable class. The input parameter infn denotes the file name of a comma-separated value (CSV) file to be loaded. In a valid CSV file, a line represents a record. An example of a line in a valid CSV file is shown below:

13,The Shawshank Redemption,1994,Frank Darabont

which has 4 fields (id, title, year, and director) separated by commas. For simplicity, assume that the 2nd (title) and 4th (director) fields would not contain commas.

This function should perform the following:

<ul>

 <li>Open the fileI/O. infn for reading. You may use either C or C++ File</li>

 <li>Read in all lines from<sub>a record) from the file into the table. When a line not following the</sub> Add every line (which corresponds to expected format is encountered, the reading of the rest of the lines is terminated.</li>

 <li>Close the file.</li>

</ul>

The function should return false if:

<ul>

 <li>The file infn does not exist or cannot be opened for reading.</li>

 <li>The filefollow the expected format.)infn is not a valid CSV file (at least one of the lines does not</li>

</ul>

Otherwise, it should return true.

Save the implementation in dbms2.cc.

(Hint: You can use the add() member function to add a line of record.) <strong>Task 6.</strong>

Completion

Provide an implementation of the member function

bool saveCSV(<strong>const char </strong>*outfn)

in the AbstractDbTable class. The input parameter outfn denotes the file name to write to.

This function should perform the following:

<ul>

 <li>Open the fileuse either C or C++ File I/O.outfn for writing. The file must be emptied. You may</li>

 <li>Write every record from the table into the file. A record must be writ-ten as a comma-separated value (see Task 5 for the specifications of a line of record.)</li>

 <li>Close the file.</li>

</ul>

The function should return false if:

<ul>

 <li>The file outfn cannot be opened for writing.</li>

 <li>Errors were encountered while writing to the file.</li>

</ul>

Otherwise, it should return true.

Save the implementation in dbms2.cc.

(Hint: You can use the get() member function to get a line of record.)

<strong>Task 7.</strong>

Challenge

Provide an implementation of LinkedListDbTable as declared in lldb.hh. Your implementation should <strong>not </strong>use the C++ standard template library. This means that you should implement the link list data structure in your code (which involves the use of C structure, pointers, and dynamic memory allocation).

Save the implementation in lldb.cc.

(Hint: Implementing a class means implementing all unimplemented member functions, constructors and destructors declared in the class declara-

tion.)

<strong>Task 8.</strong>

Challenge

Write a main() function that accepts command line arguments. Save the implementation in dbcmd.cc.

The program should perform the following:

<ol>

 <li>Create an instance of a database table. You may use either VectorDbTable or LinkedListDbTable.</li>

 <li>Load a CSV database table file named default.csv (provided).</li>

 <li>If the first command line argument is showall, it will display all rows in the table.</li>

 <li>If the first command line argument is show, then it must be followed by a second command line argument. The second argument is the row number of the record to be displayed.</li>

 <li>Destroy instance of database table.</li>

</ol>

If there are more command line arguments than required, the excess arguments are simply ignored.

To illustrate, suppose that the program is compiled as dbcmd. Suppose further that the file default.csv contains the following lines:

13,The Shawshank Redemption,1994,Frank Darabont

25,The Godfather,1972,Francis Ford Coppola

31,The Dark Knight,2008,Christopher Nolan Then if we execute

dbcmd showall

The output should be something like (depending on how you implemented the show() member function)

13 The Shawshank Redemption                             1994              Frank Darabont

25 The Godfather                                                        1972                  Francis Ford Coppola

31 The Dark Knight                                                      2008                Christopher Nolan

If we execute

dbcmd showall 100

The third argument 100 is simply ignored. Hence, the output should be the same as above.

If we execute

dbcmd show 0

The output should be something like

13 The Shawshank Redemption                             1994              Frank Darabont

which is the first row of the table. Note that row index starts from 0. If we execute

dbcmd show 100

The output should be something like

Error: Row 100 does not exist.



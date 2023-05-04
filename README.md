Download Link: https://assignmentchef.com/product/solved-csci3901-assignment1
<br>
Get practice in decomposing a problem, creating a design for a program, and implementing and testing a program.

Background

Recommender systems use past behaviours of others to give you suggestions on what has worked for others in the past, based on your own current context. Amazon books, for example, looks at the set of books that you have already purchased and compares your reading list with the reading list of others. It then aggregates the purchases of others who also bought many of the same books as you and recommends to you those books from the aggregate that you haven’t already purchased. Typically, you don’t make a recommendation unless there is enough data to suggest that it’s a meaningful recommendation.

In this assignment, we will do a simplified version of a recommender system. In our case, you will be recommending courses to take at the university based on what other students have taken.

<h2>Problem</h2>

Design a class CourseSelector that collects data on which courses students have taken, and then allows a user to make queries about the data. You will be provided with a main program that will then let a user invoke the operations on the data.

Your class will read data from a file, then allow a user to request the following three queries:

<ul>

 <li>Recommend <em>n </em>courses based on a given list of courses</li>

 <li>Print to a file the number of students who have taken any pair of courses</li>

 <li>Print to screen the number of students who have taken any pair of a given list of courses</li>

</ul>

Specifically, you will implement the following class:

<strong>class </strong>CourseSelector { <strong>public int </strong>read ( String filename ) { <em>/</em>∗ <em>IMPLEMENT </em>∗<em>/ </em>}

<strong>public </strong>ArrayList<em>&lt;</em>String<em>&gt; </em>recommend( String taken ,

<strong>int </strong>support , <strong>int </strong>numRec)

{ <em>/</em>∗ <em>IMPLEMENT </em>∗<em>/ </em>} <strong>public boolean </strong>showCommon( String          courses ) { <em>/</em>∗ <em>IMPLEMENT </em>∗<em>/ </em>}

<strong>public boolean </strong>showCommonAll( String                               filename ) { <em>/</em>∗ <em>IMPLEMENT </em>∗<em>/ </em>}

}

Descriptions of the methods follow below.

int read(String filename) The read method reads the contents of a file named filename to the object. Each line represents the courses a student has taken. The method returns the number of rows read in. The data should replace any data previously read into the class. Individual courses in a line are separated by spaces.

ArrayList&lt;String&gt; recommend(String taken, int support, int numRec) This method returns a list of numRec course recommendations given a list (taken) of courses already taken, separated by spaces. Only report courses if the recommendations are supported by at least support other students.

More specifically, the recommend method should

<ol>

 <li>Find all of the students who have taken all of the same courses listed in taken.</li>

 <li>If there are at least support students who have taken all the courses, then

  <ul>

   <li>Find all of the courses these students have taken, not including the courses listed in taken.</li>

   <li>For each of these courses, count the number of times they appear</li>

   <li>Report back the first numRec most taken courses</li>

  </ul></li>

</ol>

If you don’t have enough students to make a recommendation, then return null.

If you do have recommendations to return, then the returned ArrayList should have at most numRec in it. The courses should be provided in descending order of frequency. Two courses with the same frequency can be in any order.

There is one situation where the ArrayList can have more entries: when you reach numRec entries and there are other courses with the same frequency that you haven’t reported. Rather than choose between which of these last courses to return, report all of the ones with that frequency.

For example, suppose that the outcome of computation 2c is the following list of courses:

<table width="313">

 <tbody>

  <tr>

   <td width="82">Course</td>

   <td width="231">Number of students who have taken it</td>

  </tr>

  <tr>

   <td width="82">CSCI1100</td>

   <td width="231">12</td>

  </tr>

  <tr>

   <td width="82">CSCI2110</td>

   <td width="231">10</td>

  </tr>

  <tr>

   <td width="82">CSCI2112</td>

   <td width="231">8</td>

  </tr>

  <tr>

   <td width="82">CSCI2134</td>

   <td width="231">8</td>

  </tr>

  <tr>

   <td width="82">CSCI3110</td>

   <td width="231">5</td>

  </tr>

  <tr>

   <td width="82">CSCI3120</td>

   <td width="231">4</td>

  </tr>

 </tbody>

</table>

<ul>

 <li>For 2 recommendations, return CSCI1100 and CSCI2110.</li>

 <li>For 3 recommendations, return CSCI1100, CSCI2110, CSCI2112, and CSCI2134 (since the last two both have the same frequency).</li>

 <li>For 5 recommendations, return CSCI1100, CSCI2110, CSCI2112, CSCI2134, and CSCI3110.</li>

</ul>

boolean showCommon(String courses) This method prints to the screen a 2d array with one row and column for each course in courses in the order in which they appear. The value in each entry is the number of students who have taken both courses. Return False if any errors were encountered and True otherwise.

boolean showCommonAll(String filename) This method prints to the file filename a 2d array with one row and column for every course that has been taken by any student, in order of course name. The value in each entry is the number of students who have taken both courses. Return False if any errors were encountered and True otherwise.

Both methods with this method name compute a pairwise popularity matrix. Pairs of courses that are both taken frequently shouldn’t be scheduled at the same time, so we want to know the pairs of courses that are both taken often.

The basic logic is as follows:

<ol>

 <li>Create a 2d array with one row and one column for each course that we are given.</li>

 <li>Consider the courses of each student in our system.

  <ul>

   <li>Find the rows/column number for each of the courses.</li>

   <li>For each pair of courses, add 1 to the entry in the 2d array for the pair. Do not pair a course with itself.</li>

  </ul></li>

 <li>Print the resulting matrix.</li>

</ol>

When you print the matrix, you do not print the column names. For each row of the matrix, print the course name and then the integer from each column. Each of these bits to print will be separated by a tab character.

For example, suppose that we have entries for the following students in our system:

CSCI1110 CSCI2110 CSCI2122

CSCI2110 CSCI2112 CSCI2122 CSCI2134

CSCI1110 CSCI2134 CSCI3171

CSCI2141

If we asked for a matrix for all courses above, we would get the following output

<table width="517">

 <tbody>

  <tr>

   <td width="128">CSCI1110</td>

   <td width="64">0</td>

   <td width="64">1</td>

   <td width="64">0</td>

   <td width="64">1</td>

   <td width="64">1</td>

   <td width="64">0</td>

   <td width="7">1</td>

  </tr>

  <tr>

   <td width="128">CSCI2110</td>

   <td width="64">1</td>

   <td width="64">0</td>

   <td width="64">1</td>

   <td width="64">2</td>

   <td width="64">1</td>

   <td width="64">0</td>

   <td width="7">0</td>

  </tr>

  <tr>

   <td width="128">CSCI2112</td>

   <td width="64">0</td>

   <td width="64">1</td>

   <td width="64">0</td>

   <td width="64">1</td>

   <td width="64">1</td>

   <td width="64">0</td>

   <td width="7">0</td>

  </tr>

  <tr>

   <td width="128">CSCI2122</td>

   <td width="64">1</td>

   <td width="64">2</td>

   <td width="64">1</td>

   <td width="64">0</td>

   <td width="64">1</td>

   <td width="64">0</td>

   <td width="7">0</td>

  </tr>

  <tr>

   <td width="128">CSCI2134</td>

   <td width="64">1</td>

   <td width="64">1</td>

   <td width="64">1</td>

   <td width="64">1</td>

   <td width="64">0</td>

   <td width="64">0</td>

   <td width="7">1</td>

  </tr>

  <tr>

   <td width="128">CSCI2141</td>

   <td width="64">0</td>

   <td width="64">0</td>

   <td width="64">0</td>

   <td width="64">0</td>

   <td width="64">0</td>

   <td width="64">0</td>

   <td width="7">0</td>

  </tr>

  <tr>

   <td width="128">CSCI3171<strong>How to submit</strong></td>

   <td width="64">1</td>

   <td width="64">0</td>

   <td width="64">0</td>

   <td width="64">0</td>

   <td width="64">1</td>

   <td width="64">0</td>

   <td width="7">0</td>

  </tr>

 </tbody>

</table>
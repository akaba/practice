# Assignment 5: Software Design
### Requirements
##### 1. When starting the application, a user can choose whether to (1) log in as a specific student or (2) register as a new student.
* To register as a new student, the user must provide the following student information:
  * A unique username
  * A major
  * A seniority level (i.e., freshman, sophomore, junior, senior, or grad)
  * An email address
* The newly added student is immediately created in the system. 
* For simplicity, there is no password creation/authentication; that is, selecting or entering a student username is sufficient to log in as that student. 
* Also for simplicity, student and quiz information is local to a device.

>To handle this requirement the “Student” class with the 4 required attributes and methods added. Application will have triggers for login-as-a-specific-user and register functions which will call related methods.

>The “getRegisteredUserNames()” method will display list of existing Students to the user. If an existing Student selected, login method will log the user in as the selected Student. 

>If the user selects to create a new Student, the register method will be called to create a new Student with the required information. If the username is already exists register method will return false, prompting user that the requested userName already exists.


##### 2. The application allows students to (1) add a quiz, (2) remove a quiz they created, (3) practice quizzes, and (4) view the list of quiz score statistics.

>To fulfill this requirement “Quiz”, “Word”, ”IncorrectDefinitions”, “practiceQuiz” and “Statistics” classes included in UML design. 

>The “Quiz” and “Statistics” classes both have the “owner” attribute that holds the “userName” of “Student” class to associate each “Quiz” with a “Student”. 

>The “Statistics” class has “score” attribute to hold the practice score along with the “date” attribute that holds the date and time of practice.


##### 3. To add a quiz, a student must enter the following quiz information:
* Unique name
* Short description
* List of N words, where N is between 1 and 10,  together with their definitions 
* List of N * 3 incorrect definitions, not tied to any particular word, where N is the number of words in the quiz.

 >To fulfill this requirement “Quiz”, “Word”, ”IncorrectDefinitions” and “practiceQuiz” classes included in UML design. 

##### 4. To remove a quiz, students must select it from the list of the quizzes they created. Removing a quiz must also remove the score statistics associated with that quiz.

>“Quiz” class has the “owner” attribute that holds the “userName” of “Student’ class. Using this attribute the “viewRemoveList()” method within the student class will pull list of quizzes that active student created. The “Quiz” class includes “isCreatedBy()” method to support this process in identifying Quiz creator.

>When student makes a selection “removeQuiz(Quiz quiz)” method will be called to delete the selected quiz.

>I used composition link between “Quiz” and “Statistics” classes so removing a “Quiz” will also remove the “Statistics” associated with that quiz. 



##### 5. To practice a quiz, students must select it from the list of quizzes created by other students.

>To get list of quizzes created by other students “viewPracticeList()” method utilized which will pull list of quizzes that active student is NOT owner. The “Quiz” class includes “isCreatedBy()” method to support this process in identifying Quiz creator.



##### 6. When a student is practicing a quiz, the application must do the following:
* Until all words in the quiz have been used in the current practice session: 
  * Display a random word in the quiz word list.
  * Display four definitions, including the correct definition for that word (the other three definitions must be randomly selected from the union of (1) the set of definitions for the other words in the quiz and (2) the set of incorrect definitions for the quiz. 
  * Let the student select a definition and display “correct” (resp., “incorrect”) if the definition is correct (resp., incorrect).
* After every word in the quiz has been used, the student will be shown the percentage of words they correctly defined, and this information will be saved in the quiz score statistics for that quiz and student.


>After student selects a quiz the “practice(Quiz quiz)” method will create a new object of “practiceQuiz” class by using the data from the selected “Quiz” , “Word” and “IncorrectDefinitions” objects. 

>The “practiceQuiz” class includes the “word” as string and “fourDefinitions” as a list. Method will use this list to concatenate the correct definition with the 3 incorrect definitions that will be randomly selected from the union of “Word” and “IncorrectDefinitions” objects. 

>“PracticeShow()” method within the  “practiceQuiz” class is connected to UI and will display a random word in the quiz word list and four definitions. When user selects a definition isAnswerCorrect() method will check the answer and return true if the answer is correct and based on this result method will display “correct” or “incorrect” on UI.

>The “correctCounter” attribute initiated to zero will keep track of correct answers. After all the words has been used the “practiceEnd()” method will be called which will calculate the percentage of correct words and record this data by using the "Statistics" class.




##### 7. The list of quiz score statistics for a student must list all quizzes, ordered based on when they were last played by the student (most recent first). Clicking on a quiz must display (1) the student’s first score and when it was achieved (date and time), (2) the student’s highest score and when it was achieved (date and time), and (3) the names of the first three students to score 100% on the quiz, ordered alphabetically.

>The “Quiz” class has 5 methods to support this requirement. The student will use “viewStatistics” method to get list of all quizzes ordered based on date attribute of “Statistics” class. 

>If student makes a selection; (1) “viewFirstScore” method will display student’s first score along with the date and time, (2) “viewHighestScore” method will show student’s highest score and when it was achieve  and finally  (3) “viewTop3” method will display the names of top 3 students with 100% score ordered by alphabetically. 

> *This requirement asking to display student names, but requirement #1 does not include name for the student. So the method will display username of the student



##### 8. The user interface must be intuitive and responsive. 
>Since UI is not a class it is not displayed in the UML diagram.

##### 9. The performance of the game should be such that students do not experience any considerable lag between their actions and the response of the application.

>This is a result and  can not be included in the UML diagram.

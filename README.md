Download Link: https://assignmentchef.com/product/solved-cis573-software-engineering-homework-3
<br>
<h1>Introduction</h1>

This assignment has two parts, both related to software testing.

In the first part of the assignment, you will write JUnit tests for an Android app, using a

“mocking” library called Robolectric to mimic some of the underlying Android behavior.

In the second part of the assignment, you will conduct white-box testing on methods in a

Java Swing app. The detailed specifications will not be available, but there will be a highlevel description of the app.

You must work <strong>alone</strong> on this assignment. As before, although you are free to discuss the intent of the assignment and ask your fellow classmates for clarification, the code and report that you write must be your own.

This assignment is worth a total of 100 points.




<h1>Part 1. Android Testing</h1>

In this part of the assignment, you’ll write tests for an Android app.




<h2>Implementation</h2>

The app that you’ll test is a slightly modified implementation of the Traveling Salesman game from Homework #2. You can download the app as an Android Studio project in Canvas. Please use this implementation, and not the one from Homework #2; also, please note that this is <em>not</em> a solution to Homework #2, of course.




The classes in this app are more or less the same as in Homework #2, except that the GameView class now has a separate method for detecting circuits (<em>detectCircuit</em>).







<h2>Setting Up</h2>

As discussed in class, there are generally two ways to write tests for Android apps:

<ul>

 <li>“Android Instrumentation Tests,” which run in the context of the full Android OS and require some sort of underlying device (physical or virtual)</li>

 <li>“JUnit Tests,” which can still test Android classes but require some library to mock the underlying OS behavior</li>

</ul>




In this assignment, you will write JUnit Tests, using the Robolectric library for mocking the Android components. Be sure to review your class notes from the lecture on Android testing if you need help.




To get your JUnit Tests set up in Android Studio, follow these steps:

<ol>

 <li>Build the TravelingSalesman-testMe project and make sure you can run it in a virtual device (just like in Homework #2) before proceeding.</li>

 <li>In Android Studio, choose File -&gt; Project Structure… from the main menu. Then choose Project from the menu on the left and then set <strong>Android Plugin Version to 1.1.3</strong> as shown below (if it’s already higher, leave it as-is):</li>

</ol>




<img decoding="async" data-recalc-dims="1" data-src="https://i0.wp.com/www.ankitcodinghub.com/wp-content/uploads/2018/03/297.png?w=980&amp;ssl=1" class="lazyload" src="data:image/gif;base64,R0lGODlhAQABAAAAACH5BAEKAAEALAAAAAABAAEAAAICTAEAOw==">

 <noscript>

  <img decoding="async" src="https://i0.wp.com/www.ankitcodinghub.com/wp-content/uploads/2018/03/297.png?w=980&amp;ssl=1" data-recalc-dims="1">

 </noscript>




<ol start="3">

 <li>Modify the build.gradle file for the “app” module as shown in the screen capture on the next page:

  <ul>

   <li>Add <strong>testOptions {unitTests.returnDefaultValues = true} </strong>to the “android” configuration. This tells Android Studio that we are going to mock the underlying Android components.</li>

   <li>Add <strong>testCompile ‘junit:junit:4.12’ </strong>to the “dependencies” configuration. This tells Android Studio that we’re going to need JUnit 4.12.</li>

   <li>Add <strong>testCompile ‘org.robolectric:robolectric:3.0-rc2’ </strong>to the “dependencies” configuration. This tells Android Studio that we’re going to use the Robolectric library.</li>

  </ul></li>

 <li>After making these changes,<strong> choose Build -&gt; Make Project from the main menu</strong>. This will likely cause Android Studio to download JUnit and Robolectric, so be sure you are connected to the Internet when you do this. This may take a few minutes to finish and you should eventually see “Gradle build finished” in the bottom left message bar (if you get warnings, choose the “Messages” tab and if there’s something there about commons-logging, it’s okay to ignore that).</li>

</ol>

<img decoding="async" data-recalc-dims="1" data-src="https://i0.wp.com/www.ankitcodinghub.com/wp-content/uploads/2018/03/515.png?w=980&amp;ssl=1" class="lazyload" src="data:image/gif;base64,R0lGODlhAQABAAAAACH5BAEKAAEALAAAAAABAAEAAAICTAEAOw==">

 <noscript>

  <img decoding="async" src="https://i0.wp.com/www.ankitcodinghub.com/wp-content/uploads/2018/03/515.png?w=980&amp;ssl=1" data-recalc-dims="1">

 </noscript>







<ol start="5">

 <li>Next we’ll tell Android Studio that we’re going to use “JUnit Tests” instead of “Android Instrumentation Tests.” Select the Build Variants tab (it’s probably on the bottom left of the window, and the words are vertical). In the Build Variants window, <strong>change Test Artifact from “Android Instrumentation Tests” to “Unit Tests” </strong>as shown below:</li>

</ol>




<img decoding="async" data-recalc-dims="1" data-src="https://i0.wp.com/www.ankitcodinghub.com/wp-content/uploads/2018/03/258.png?w=980&amp;ssl=1" class="lazyload" src="data:image/gif;base64,R0lGODlhAQABAAAAACH5BAEKAAEALAAAAAABAAEAAAICTAEAOw==">

 <noscript>

  <img decoding="async" src="https://i0.wp.com/www.ankitcodinghub.com/wp-content/uploads/2018/03/258.png?w=980&amp;ssl=1" data-recalc-dims="1">

 </noscript>




<ol start="6">

 <li>Choose <strong>Build -&gt; Make Project</strong> from the main menu to rebuild the project.</li>

 <li>Next you need to create a directory to hold your JUnit tests. You should <em>not</em> use the built-in “androidTest” directory, but rather should create a new one. Open the Project view in the top left (it may currently be set to the Android view) and then <strong>create a subdirectory called test, then test/java/ in the app/src/ directory</strong>. You should see the java subdirectory turn green.</li>

</ol>

<img decoding="async" data-recalc-dims="1" data-src="https://i0.wp.com/www.ankitcodinghub.com/wp-content/uploads/2018/03/610.png?w=980&amp;ssl=1" class="lazyload" src="data:image/gif;base64,R0lGODlhAQABAAAAACH5BAEKAAEALAAAAAABAAEAAAICTAEAOw==">

 <noscript>

  <img decoding="async" src="https://i0.wp.com/www.ankitcodinghub.com/wp-content/uploads/2018/03/610.png?w=980&amp;ssl=1" data-recalc-dims="1">

 </noscript>




<ol start="8">

 <li>Now go back to the Android view and open the GameActivity class in the code editor. Right-click on the class name in the code (i.e., the line that reads “public class GameActivity extends ActionBarActivity”), then <strong>select Go To from the context menu, then choose Test, then Create new test…</strong></li>

 <li><strong>Select JUnit 4 as the Testing library</strong>, name the class <strong>GameActivityTest</strong>, and click OK.</li>

</ol>




<ol start="10">

 <li><strong>Replace the code for GameActivityTest with the code from Canvas</strong>. This code is configured to use the Robolectric library but otherwise is just a standard JUnit test class. It has placeholders for the test methods you need to implement.</li>

 <li>Choose Build -&gt; Make Project from the main menu to rebuild the project.</li>

 <li>In the Android v<img decoding="async" data-recalc-dims="1" data-src="https://i0.wp.com/www.ankitcodinghub.com/wp-content/uploads/2018/03/147-1.png?w=980&amp;ssl=1" class="lazyload" src="data:image/gif;base64,R0lGODlhAQABAAAAACH5BAEKAAEALAAAAAABAAEAAAICTAEAOw==">

  <noscript>

   <img decoding="async" src="https://i0.wp.com/www.ankitcodinghub.com/wp-content/uploads/2018/03/147-1.png?w=980&amp;ssl=1" data-recalc-dims="1">

  </noscript>iew, <strong>right-click GameActivityTest.java and choose Run GameActivityTest. </strong>You should see the unit test run in the console on the bottom left and then see the message “All Tests Passed”:</li>

</ol>

<img decoding="async" data-recalc-dims="1" data-src="https://i0.wp.com/www.ankitcodinghub.com/wp-content/uploads/2018/03/430.png?w=980&amp;ssl=1" class="lazyload" src="data:image/gif;base64,R0lGODlhAQABAAAAACH5BAEKAAEALAAAAAABAAEAAAICTAEAOw==">

 <noscript>

  <img decoding="async" src="https://i0.wp.com/www.ankitcodinghub.com/wp-content/uploads/2018/03/430.png?w=980&amp;ssl=1" data-recalc-dims="1">

 </noscript>




If you made it this far, you’re ready to start writing your own tests!




<strong>Troubleshooting: </strong>

<ul>

 <li>Error running GameActivityTest: Class edu.upenn.cis573.travelingsalesman.GameActivityTest not found in module ‘app’ o Be sure to select “Unit Tests” for the Test Artifact in the Build Variants panel, and not “Android Instrumentation Tests”</li>

 <li>lang.RuntimeException: Method setUp in android.test.ActivityUnitTestCase not mocked. o Make sure you add the testOptions configuration in build.gradle for the app module</li>

 <li>lang.RuntimeException:</li>

</ul>

build/intermediates/bundles/debug/AndroidManifest.xml not found or not a file o This may happen on a Mac. To fix it, do the following:

<ul>

 <li>§ Go to Run -&gt; Edit Configurations</li>

 <li>§ On the left, choose JUnit then GameActivityTest</li>

 <li>§ Set Working Directory to $MODULE_DIR$</li>

 <li>Gradle: Error: Cannot find symbol class GameActivity o You should be able to make this go away by choosing Build -&gt; Clean Project and then Build -&gt; Make Project</li>

 <li>Exception in thread “main” java.lang.NoClassDefFoundError:</li>

</ul>

junit/textui/ResultPrinter o You can ignore this… just re-run your test <strong>Testing Activities </strong>

Implement these unit tests in GameActivityTest:

<ol>

 <li><em>testCreateSegment</em>: tests that a line segment is properly created and added to the collection of segments in the GameView when the user touches the screen close to one of the map locations (within 30 pixels), drags their finger close to another location, and releases</li>

 <li><em>testDontCreateSegmentFirstPointNotCloseToMapLocation</em>: tests that a line segment is <em>not</em> added to the collection of segments when the user’s touch is not close (within 30 pixels) to one of the map locations, then they drag their finger close to another location and releases</li>

 <li><em>testDontCreateSegmentLastPointNotCloseToMapLocation</em>: tests that a line segment is <em>not</em> added to the collection of segments when the user’s touch is close to one of the map locations, then they drag their finger and release at a point that is not close to a map location</li>

 <li><em>testDontCreateSegmentFirstAndLastPointsSame</em>: tests that a line segment is <em>not</em> added to the collection of segments when the user’s touch is close to one of the map locations, then they drags their finger and release close to the same map location</li>

 <li><em>testDontCreateCircuit</em>: tests that the <em>detectCircuit</em> method returns false when the number of line segments equals the number of map locations, but the line segments do not form a single circuit (you do not have to worry about the “two circuit” problem that you fixed in Homework #2).</li>

 <li><em>testCreateCircuitNotShortestPath</em>: test that the <em>detectCircuit </em>method returns true when the number of line segments equals the number of map locations and the line segments form a circuit, but that the value returned by <em>myPathLength</em> is not the same as the distance for the shortest path for that set of map locations.</li>

 <li><em>testCreateCircuitShortestPath</em>: test that the <em>detectCircuit </em>method returns true when the number of line segments equals the number of map locations and the line segments form a circuit, and that the value returned by <em>myPathLength</em> is the same (within 0.01) as the distance for the shortest path.</li>

</ol>

<strong> </strong>

Notes:

<ul>

 <li>For tests 1-4, you can directly manipulate the <em>mapPoints</em> field and then directly inspect the <em>segments </em> You do, however, need to use MotionEvents to simulate the user touching the screen and moving their finger. See the Android Testing lecture slides for an example of how to do this.</li>

 <li>For tests 5-7, you can directly manipulate the <em>segments</em> field, i.e. you don’t have to simulate MotionEvents.</li>

 <li>For test 1 (<em>testCreateSegment</em>), keep in mind that it is not sufficient to check that another line segment has been added to the <em>segments</em> field; you must check that the segment connects the correct points. It’s a little tricky, though: the values held in <em>mapPoints</em> represent the top left corner of the square that is drawn onscreen, whereas the values held in <em>segments</em> refer to the center of the square and are shifted by 10 pixels on the x- and y-axes from the values in <em>mapPoints</em>.</li>

 <li>You may <em>not</em> refactor or modify the implementation of the TSP app in order to write your unit tests. Please notify the instructor if you feel that it is necessary to do so.</li>

 <li>If written correctly, all of these tests should pass! If you believe that your test is sound but the test fails, please notify the instructor.</li>

</ul>







<h1>Part 2. White-Box Testing</h1>

Presumably you have heard of the game Hangman, in which one player thinks of a word and the other tries to guess it by suggesting letters. If the player cannot figure out the word in a certain number of guesses, then he or she loses. See http://en.wikipedia.org/wiki/Hangman_(game) if you are not familiar with this game.




You may have had something like this as an introductory programming assignment, in which the computer program randomly picks a word and the human player has to guess it.

In 2011, a variation of this game was presented at the SIGCSE conference on computer science education. In this variation, called “Evil Hangman”

(http://nifty.stanford.edu/2011/schwarz-evil-hangman/), the computer program changes the target word according to what letters the human player has suggested, making it very hard to correctly guess the word. Sneaky, huh?




The “evil” program works by maintaining a list of words and then, each time the player suggests a letter, removing all words containing that letter from its list (assuming that some words would still remain), essentially dodging the human player’s guesses as much as possible. Although it is possible for the human player to win, it is certainly tricky to do so.




In this assignment, you are given an implementation of Evil Hangman and you need to conduct white-box testing of three methods.

<strong> </strong>

<h2>Implementation</h2>

The code that you will test is available in Canvas. We recommend that you use Eclipse for this part of the assignment.




The app that you will test uses the Java Swing API for its user interface; if you haven’t encountered Swing before, it’s pretty similar to Android in that you have objects to represent the window itself (in Swing, these are called JFrames), you have the various UI widgets (e.g. JLabel, JComboBox, JButton, etc.), and you have methods that are called whenever the user interacts with a widget (this method is usually called “actionPerformed”).




There are four classes that represent the different windows that appear in the app:

<ul>

 <li><strong>Start</strong>: This is shown when the application starts. It contains drop-down lists to allow the user to choose the number of letters in the target word and the</li>

</ul>

maximum number of incorrect guesses allowed. This contains the “main” method for the program, too.

<ul>

 <li><strong>GUI_PlayGame</strong>: This is the window in which the user plays the game by clicking on buttons for the different letters.</li>

 <li><strong>GUI_Winner</strong>: This window is shown when the user correctly guesses the word. You won’t be seeing it much. &#x1f609;</li>

 <li><strong>GUI_Loser</strong>: This is shown when the user runs out of letters to guess.</li>

</ul>

<strong> </strong>

There are three other classes that represent the data and logic for playing the game:

<ul>

 <li><strong>HangmanGame</strong>: This is an interface that defines the methods needed in order to play hangman.</li>

 <li><strong>NormalHangMan</strong>: This is an implementation of the interface that plays hangman by the normal rules.</li>

 <li><strong>EvilHangMan</strong>: This is an implementation that changes the target word each time the player makes a guess.</li>

</ul>




This app starts out by using EvilHangMan as the HangmanGame implementation; however, if the player guesses a letter, and removing all words with that letter would mean there are no legal words left, then that guess is considered to be correct

(EvilHangMan may be evil, but it’s not a cheater). At that point, the app chooses one of the legal words from the dictionary and switches over to NormalHangMan rules.




<h2>Testing Activities</h2>

In this part of the assignment, you need to write <strong>JUnit tests</strong> for these three methods:

<ul>

 <li>makeGuess</li>

 <li>makeGuess</li>

 <li>controller</li>

</ul>




Please use JUnit 4 for your test cases, and follow the naming conventions discussed in class.




Your goal is to create a set of unit tests that achieves <strong>100% statement coverage</strong> for each method.




Note that GUI_PlayGame.controller calls makeGuess, but you still need separate unit tests for the two makeGuess methods anyway. That is, when you run your tests for controller, you’ll also cover some statements in makeGuess, but you cannot count those toward the statement coverage for makeGuess. You are expected to have a separate set of tests for each makeGuess method, and those tests should achieve 100% statement coverage.




Keep in mind that it is not enough just to have tests that call each method with various inputs so that the different statements are covered; <strong>your tests must be sound</strong> and <strong>must check for any visible side effects </strong>(i.e., changes to public or protected fields) of calling the method, as well as its return value. This means that for GUI_PlayGame.controller, your tests must check that the JLabels have the right values (hint: use the “getText” method) and that the HangmanGame field is properly set up; you do not, however, need to check that the Winner or Loser screen was displayed.




Please note that you should <em>not</em> change the implementation of any classes that we provided in order to write your tests. If you think a change is necessary, please speak with a member of the instruction staff.




<h2>Measuring Coverage</h2>

To measure the statement coverage achieved by your unit tests, we recommend you use CodePro <u>(</u><u>https://developers.google.com/java-dev-tools/codepro/doc/</u>), which may already be bundled with your Eclipse distribution. Open the Package Explorer of your Java project and right-click on a .java file to open the context menu. If you see “Coverage As” toward the bottom of the menu, you’re all set.




Otherwise, to install the CodePro plugin on your own machine, follow these instructions:

<ul>

 <li>In Eclipse, click the Help menu.</li>

 <li>Click “Install New Software…” or a similar option in older versions</li>

 <li>Click “Add…”</li>

 <li>For the “Name” field, put “CodePro”</li>

 <li>In the “Location” field, enter “http://dl.google.com/eclipse/inst/codepro/latest/3.7” if you are using Eclipse 3.7 or later, and</li>

</ul>

“http://dl.google.com/eclipse/inst/codepro/latest/3.6” if you have 3.6

<ul>

 <li>Click OK</li>

 <li>You should now see CodeCoverage, CodePro, and Infrastructure as installation options</li>

 <li>Click “Select All”</li>

 <li>Click “Next”</li>

 <li>Agree to all the license agreements</li>

 <li>Click “Finish” and wait a few minutes for it to install</li>

 <li>Exit and restart Eclipse (it should prompt you to do this, if not, do it manually).</li>

</ul>




Once CodePro is installed, you can measure coverage by right-clicking on the name of your JUnit test class, then choosing “Coverage As” from the context menu, and then “JUnit Test.”




You should see a new panel open at the bottom of Eclipse that allows you to navigate to your source code and see the amount of coverage that was achieved.




If you open the code in the code editor window, you’ll see covered statements in green and uncovered statements in red. Yellow statements are decision points for which branches have only been partially covered; you can consider these as “covered” for our purposes.

<strong> </strong>

Some students have had difficulty getting CodePro to work on Eclipse 3.7 and later. Feel free to use other coverage tools such as <u>EclEmma</u> (<u>http://www.eclemma.org</u>) or <u>eCobertura</u> (<u>http://ecobertura.johoop.de/</u>). Instructions will be posted in Canvas.

If some statements cannot be covered, create a plain-text README file and explain why the statements are unreachable, e.g. by stating the unsatisfiable path condition.







<strong><u>A few words about using Piazza…</u> </strong>

As always, please be careful about how you use Piazza for this assignment. It is important that you do not reveal (accidentally or intentionally) which test cases you’ve created or how you wrote them.




Please use Piazza for (a) clarification questions regarding the intent of the assignment, (b) clarification questions regarding the specification of the code you’re testing, and (c) getting help with problems using Android Studio, Robolectric, JUnit, coverage tools, etc.




Before you post anything on Piazza, think to yourself “is my question giving away an answer?” If you think it is, please email the instruction staff directly and we’ll post it if we think it’s appropriate.









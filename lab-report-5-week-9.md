# Lab Report 5 - Week 9
For this week's lab report we were given the task of creating a grading script. This is similar to the autograder scripts that run on gradescrope for other courses such as cse12 so it was cool learning how to create our very own autograders. Creating the grading script was actually pretty challenging and called up learning lots of new ways to use different command line tools such as `grep`,learning `if` statements in bash, and also learning how to create and use variables. It was cool to see the behind the scenes that goes down in those gradescope autograders that grade our code.

## Grading Script
In lab 7 we were tasked to work with a partner to create a grading script. I worked together with Sherif Elfiky to come up with our grading script.
```
JU=".:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar"

rm -rf student-submission
git clone $1 student-submission

echo "Successful clone"

FILE=student-submission/ListExamples.java

if  [ -f "$FILE" ]; then
    echo "file exists"
else
    echo "ListExamples.java was not found."
    echo "You recieve a score of: 0 / 2"
    echo "Check that your file is named properly and that your file is not nested."
    exit 1
fi

cp -r lib student-submission
echo "Junit copied"

cp TestListExamples.java student-submission/
cd student-submission
echo "In student-submission"

# Score of the tests. Starts at value 0 and increases
# when qualifications are met.
# out of 2
SCORE=0

javac -cp $JU *.java 2> CompileErr.txt
if [[ $? -ne 0 ]]; then
    echo "Your code did not compile. You recieve a $SCORE / 2"
    exit 1
fi
echo "Compiled"

echo "--> Beginning tests now <--"

java -cp $JU org.junit.runner.JUnitCore TestListExamples > JunitOut.txt

grep -q "2 tests" JunitOut.txt
if [[ $? -eq 0 ]]; then
    SCORE=2
fi
grep -q "Failures: 1" JunitOut.txt
if [[ $? -eq 0 ]]; then
    SCORE=1
fi


echo "Your score is: $SCORE / 2"
if [[ $SCORE -eq 2 ]]; then
    echo "Great job! All tests passed!"
fi
if [[ $SCORE -eq 1 ]]; then
    echo "Uh Oh! A test is failing! Revise your code."
fi
```

## Screenshots on Local Server
Repository: https://github.com/ucsd-cse15l-f22/list-methods-lab3
![Image](week-9-screenshots/fails-one.png)

Repository: https://github.com/ucsd-cse15l-f22/list-methods-corrected
![Image](week-9-screenshots/correct.png)

Repository: https://github.com/ucsd-cse15l-f22/list-methods-filename
![Image](week-9-screenshots/wrong-name.png)

## Tracing the grading script
For this trace we will be examining the following repository, https://github.com/ucsd-cse15l-f22/list-methods-corrected , which recieved a score of 2/2. A full score!


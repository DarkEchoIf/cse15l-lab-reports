# CSE15L Lab Report Week 8: Finale
## My grade.sh
```
#set -e
CPATH=".:../lib/hamcrest-core-1.3.jar:../lib/junit-4.13.2.jar"
Score=0
rm -rf student-submission
git clone $1 student-submission
cd student-submission

if [[ -f ListExamples.java ]]
then
  echo "found the file"
  ((Score+=1))
else
   echo "file not found"
 fi

cd ..
cp TestListExamples.java student-submission

cd student-submission
javac -cp $CPATH *.java 2>compile-error.txt
if [[ $? -eq 0 ]]
then
  echo "compilations successful"
  ((Score+=1))
else
  echo "compilations failed"
fi

java -cp $CPATH org.junit.runner.JUnitCore TestListExamples 2 > results.txt
if [[ $? -ne 0 ]]
then
  echo "Failed tests"
  exit 1
else
  echo "Passed all tests"
  ((Score+=1))
  echo "Total Point: [$Score/3 points]"
  exit 0
fi
```
## My Failed Case
![grade.sh](grade.sh%20bash.png) 
Utill the end, I was not able to implement my grade.sh completely; and due to the constraint of time, it won't be completed before the deadline of the report. Base on that fact, I would still like to analyze my grade.sh, to see what works and what caused it to fail, so I can learn from this failed case.

If we regard 'CPATH=...' as the first line of grade.sh, line 1 to 6 is the set up for the grader. I first defined 'CPATH', which will save me time from repeatedly typing long directory/library. I also set 'Score=0' as the counter of grades. Both of them do not generate stdout or stderr.

The 'rm -rf...' line ensures the reusability of the script. It does not generate stdout or stderr either.

'git clone' grabs the codes to be graded form the given url. It's behaviour is represented in the stdout from the 'Cloning into...' line to the 'Receiving Objects...' line.

Line 7 to 13 is a 'if-fi' block that checks if the cloned repository contians the required files. When the file exist, 'Score' will have a increment', while stdout 'found the file' is printed. Otherwise, stdout 'file not found' is printed. In my case, the if statement is true.

After some directory change and file transfering in line 15, 16, and 18, we compile all the files in 'student submission' and checks if the compilations are successful in line 19 to 26. Similar to the previous 'if-fi' block, both if and else situation will print a message to stdout. Addtionally, if the file failed to compile, the error message won't be printed because it is directed to 'compile-error.txt'. In my case, the if statement is true.

Line 28 run the TestListExamples.java and directed all its output to 'result.txt'. Here is where the problem start:
![Results](grade.sh%20test_results.png) 

Due to my failed implementation of TestListExamples.java, I got error messages shown above and even the nearly perfectly implemented student submission won't be able to pass in my grader.

Originally, the 'if-fi' block that comes after line 28 should give feedback about whether the tests were passed, if so, also generate the score. However, since my TestListExamples.java always generate error, the block will also always respond:'Failed tests'.

To sum up, if I could have a correct TestListExamples.java implementation, the grade.sh script should be able to fulfil its expected role. The cause for the error in TestListExamples.java requires further inspection, and won't be covered in this report.
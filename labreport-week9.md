# Lab Report - Week 9

For this lab report, I created an autograder, which is a bash script that would grade the code in a GitHub repo

**Autograder -> `grade.sh`**

```
rm -rf student-submission
git clone $1 student-submission

CP=.:../lib/hamcrest-core-1.3.jar:../lib/junit-4.13.2.jar
CP2=.:../lib/hamcrest-core-1.3.jar:../lib/junit-4.13.2.jar

cp TestListExamples.java student-submission

cd student-submission

if [[ ! -e ListExamples.java ]]
then
    echo "ListExamples.java does not exist in the directory"
    exit 1
fi

javac -cp $CP *.java 2> err.txt

if [[ ! $? -eq 0 ]]
then
    echo "Cannot compile ListExamples and/or TestListExamples!"
    cat err.txt
    exit 1
fi

javac -cp $CP *.java
java -cp $CP2 org.junit.runner.JUnitCore TestListExamples > output.txt

if [[ $? -eq 0 ]]
then
echo "You passed all tests"
else
head -20 output.txt 
failed="$(grep -w Failures output.txt)"
echo $failed
echo "Your total score is" "$((${failed:25:1}-${failed:11:1}))" "out of ${failed:11:1}"
fi

exit 0
```

## **How grade.sh works**

1. Clones GitHub repo and stores ListExamples.java code in student-submission folder

2. Pulls ListExamples from folder student-submission (if statement to check if it existed in github repo that was pulled)

3. Compiles ListExamples and TestListExamples (java file with test cases for ListExamples)

4. Returns error output if at least one of the tests fails, will return tests ran and how many failed, and the total score

## **Three different repos for autograder**


[Index](https://zcashe.github.io/cse15l-lab-reports/index.html)
---
# Lab Report 5 
---
# Part 1 – Debugging Scenario

This is inspired by something that actually happened during one of my labs. 

## Original Edstem Post 
Ed Stem Post (as student)
```
Hello I need help on my lab 7 report, I'm trying to run the grading script on my find command,
however I get this error

I think it might have something to do with my find command searching to far,
but I'm not using -r so I don't think its recursive.




I am just trying to find and store the filename using submission=$(find / -name "*.java")
then I am trying to compile it by using javac -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar submission.

Any Suggestions?
```
 
<img width="678" alt="Screenshot 2024-03-12 at 10 25 14 PM" src="https://github.com/zcashe/cse15l-lab-reports/assets/96392105/d18eea9e-ab31-42be-b74c-79d10588d920">


## TA Response
```
I think that your find command is being used incorrectly,
can you try instead of using / use find "(file_directory)" -name "*.java".
Let me know how that goes and if your problem gets solved.
```




## Screenshot from using the help and Bug description

> OK I used your solution here, however it still seems to have this weird effect. I don't understand why it won't compile.

<img width="711" alt="Screenshot 2024-03-12 at 10 39 06 PM" src="https://github.com/zcashe/cse15l-lab-reports/assets/96392105/76166c6e-f0c2-4b56-b395-14667587d680">




Bug Description:
> This is a 2 part bug, the first part was the find command finding too many files and not the proper java file inside my directory which I got help with.

<img width="704" alt="Screenshot 2024-03-12 at 11 09 16 PM" src="https://github.com/zcashe/cse15l-lab-reports/assets/96392105/ac39372a-5f7f-419f-a4e9-6eff6d567c1f">

> After the ta helps and the submission variable echos out the correct pass, it doesn't properly compile.
> The second part is that even once the first part finds the correct file the compilation fails and it gives and error.

## File Structure
```
├── JavaLab
│   ├── ListExamples.java
│   └── ListExamplesTests.java
├── grade.txt
├── junit-output.txt
├── lib
│   ├── hamcrest-core-1.3.jar
│   └── junit-4.13.2.jar
└── test.sh
```

## File Contents
ListExamples.java
```
import java.util.ArrayList;
import java.util.List;

interface StringChecker { boolean checkString(String s); }

class ListExamples {

  static List<String> filter(List<String> list, StringChecker sc) {
    List<String> result = new ArrayList<>();
    for(String s: list) {
      if(sc.checkString(s)) {
        result.add(0, s);
      }
    }
    return result;
  }

  static List<String> merge(List<String> list1, List<String> list2) {
    List<String> result = new ArrayList<>();
    int index1 = 0, index2 = 0;
    while(index1 < list1.size() && index2 < list2.size()) {
      if(list1.get(index1).compareTo(list2.get(index2)) < 0) {
        result.add(list1.get(index1));
        index1 += 1;
      }
      else {
        result.add(list2.get(index2));
        index2 += 1;
      }
    }
    while(index1 < list1.size()) {
      result.add(list1.get(index1));
      index1 += 1;
    }
    while(index2 < list2.size()) {
      result.add(list2.get(index2));
      // change index1 below to index2 to fix test
      index1 += 1;
    }
    return result;
  }
}
```

ListExamplesTests.java
```
import static org.junit.Assert.*;
import org.junit.*;
import java.util.*;
import java.util.ArrayList;

public class ListExamplesTests {
	@Test
	public void testMerge1() {
    		List<String> l1 = new ArrayList<String>(Arrays.asList("x", "y"));
		List<String> l2 = new ArrayList<String>(Arrays.asList("a", "b"));
		assertArrayEquals(new String[]{ "a", "b", "x", "y"}, ListExamples.merge(l1, l2).toArray());
	}
	
	@Test
        public void testMerge2() {
		List<String> l1 = new ArrayList<String>(Arrays.asList("a", "b", "c"));
		List<String> l2 = new ArrayList<String>(Arrays.asList("c", "d", "e"));
		assertArrayEquals(new String[]{ "a", "b", "c", "c", "d", "e" }, ListExamples.merge(l1, l2).toArray());
        }

}
```

grade.txt
```
{empty because code fails}
```

junit-output.txt
```
{Empty Doesn't run}
```

test.sh
```
submission=$(find / -name "*.java")

javac -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar submission

if [[ $? -ne 0 ]]
then 
    echo "didn't compile"
    echo " Grade: DIDNT COMPILE " >> grade.txt
    exit 1
fi

java -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar org.junit.runner.JUnitCore ListExamplesTests > junit-output.txt

lastLine=$(cat junit-output.txt | tail -n 2)

echo $lastLine

if grep -q "OK" junit-output.txt;
then 
    echo "Grade: 100%" >> grade.txt
    exit 0
fi
tests=$(grep -o "Tests run: [0-9]*" junit-output.txt | cut -d' ' -f3)

failures=$(grep -o "Failures: [0-9]*" junit-output.txt | cut -d' ' -f2)

successful_tests=$((tests - failures))

rate=$((succesful_tests / tests))

hundredrate=$((rate * 100))

gradescript="Final grade is $hundredrate %"

echo $gradescript >> grade.txt
```

## Command Line arguments to get bug

>The bug occurs when running the bash script with ```bash test.sh```

## How to Fix the bug

>So this is a multilayered bug. First I needed to correct the submission variable

>```submission=$(find "JavaLab" -name "*.java")``` instead of ```submission=$(find / -name "*.java")```
>The original was searching in the wrong directory for the java files, but the second one searches just the JavaLab directory.

>Then in the compilation stage, I fix it by having 
>```javac -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar $submission``` instead of ```javac -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar submission```

>In Bash the variables need to be marked with a $ if they are going to be used inside of a command like this. Otherwise it doesn't recognize it as a variable.

>Then once you do all this the code works perfectly, so it was a mix of incorrect command usage and bash syntax issues.

>(Note: The actual java test is meant to fail so I can test that when the bash script runs properly it gives the accurate result 50%)

---
# Part 2 - Reflection

>In the second half of the quarter I learned a lot about using the command line. The bash scripting and java command processes are very interesting, although
I do really struggle remembering the bash syntax. However I recognize the use and how important it can be for creating and running scripts. Using the java debugger is also something I learned how to do
and it seems really useful especially for when I have long complicated code and need to understand what all the variables are doing. 
Overall I feel as though I learned a lot of this quarter and want to learn even more. Unrelated to the labs I also learned a lot about the tutoring process, and now I think I want to try to become a tutor for a CSE class for summer quarter. It seems fun and I like helping people with their code so I think I could enjoy it.


Thanks for your hard work grading this quarter! 

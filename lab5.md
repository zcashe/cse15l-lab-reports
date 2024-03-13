[Index](https://zcashe.github.io/cse15l-lab-reports/index.html)
---
# Lab Report 5 
---
# Part 1 – Debugging Scenario

## Original Edstem Post 
![Image](assets/lab-report4/ieng4.png)
 


## TA Response
![Image](assets/lab-report4/ieng4.png)


## Screenshot from using the help and Bug description

> OK I used your solution here, however it still seems to have this weird effect.


> Bug Description:
> 

## File Structure
```
├── ListExamples.class
├── ListExamples.java
├── ListExamplesTests.class
├── ListExamplesTests.java
├── StringChecker.class
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
Final grade is 0 %
```

junit-output.txt
```
JUnit version 4.13.2
..E
Time: 11.615
There was 1 failure:
1) testMerge2(ListExamplesTests)
java.lang.OutOfMemoryError: Java heap space
	at java.base/java.util.Arrays.copyOf(Arrays.java:3513)
	at java.base/java.util.Arrays.copyOf(Arrays.java:3482)
	at java.base/java.util.ArrayList.grow(ArrayList.java:237)
	at java.base/java.util.ArrayList.grow(ArrayList.java:244)
	at java.base/java.util.ArrayList.add(ArrayList.java:483)
	at java.base/java.util.ArrayList.add(ArrayList.java:496)
	at ListExamples.merge(ListExamples.java:42)
	at ListExamplesTests.testMerge2(ListExamplesTests.java:19)
	at java.base/java.lang.invoke.LambdaForm$DMH/0x00000008000c2400.invokeVirtual(LambdaForm$DMH)
	at java.base/java.lang.invoke.LambdaForm$MH/0x00000008000c3000.invoke(LambdaForm$MH)
	at java.base/java.lang.invoke.Invokers$Holder.invokeExact_MT(Invokers$Holder)

FAILURES!!!
Tests run: 2,  Failures: 1
```

test.sh
```
javac -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar *.java

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

failures=$(grep -o "Tests run: [0-9]*" junit-output.txt | cut -d' ' -f2)

successful_tests=$((tests - failures))

rate=$((succesful_tests / tests))

hundredrate=$((rate * 100))

gradescript="Final grade is $hundredrate %"

echo $gradescript >> grade.txt
```

## Command Line arguments to get bug


## How to Fix the bug



---
# Part 2 - Reflection

In the second half of the quarter I learned a lot about using the command line. The bash scripting and java command processes are very interesting, although
I do really struggle remembering the bash syntax. However I recognize the use and how important it can be for creating and running scripts. Using the java debugger is also something I learned how to do
and it seems really useful especially for when I have long complicated code and need to understand what all the variables are doing. 
Overall I feel as though I learned a lot of this quarter and want to learn even more.

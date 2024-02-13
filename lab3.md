[Index](https://zcashe.github.io/cse15l-lab-reports/index.html)
---
# Lab 3 Report 
---
# Part 1 Bug Testing

## Non-Failing Test:
```
@Test 
public void testReverseOne() {
    int[] singleArr = { 1 };
    ArrayExamples.reverseInPlace(singleArr);
    assertArrayEquals(new int[]{  }, singleArr);
}
```



## Failing Test:
```
@Test
public void testReverseReal(){
    int[] numArr = {1,2,3};
    ArrayExamples.reverseInPlace(numArr);
    assertArrayEquals(new int[]{3,2,1}, numArr);
}
```

## Symptom:
![Image](assets/IMG_1506.jpeg)

## The Bug:
Before:
```
static void reverseInPlace(int[] arr) {
    for(int i = 0; i < arr.length; i += 1) {
      arr[i] = arr[arr.length - i - 1];
    }
  }
```
After:
```
static void reverseInPlace(int[] arr) {
    for(int i = 0; i < arr.length; i += 1) {
      arr[i] = arr[arr.length - i - 1];
    }
  }
```


---
# Part 2 Exploring find


## Command 1 - find -name
Example 1: find technical/ -name 'preface.*'

Source: [https://man7.org/linux/man-pages/man1/find.1.html](https://man7.org/linux/man-pages/man1/find.1.html)

```
zac@Zacs-MacBook-Pro docsearch % find technical/ -name 'preface.*'
technical//911report/preface.txt
zac@Zacs-MacBook-Pro docsearch % 
```
>Explanation:

Example 2: find technical/ -name 'chapter*.txt'

Source: [https://man7.org/linux/man-pages/man1/find.1.html](https://man7.org/linux/man-pages/man1/find.1.html)
```
zac@Zacs-MacBook-Pro docsearch % find technical/ -name 'chapter*.txt'
technical//911report/chapter-13.4.txt
technical//911report/chapter-13.5.txt
technical//911report/chapter-13.1.txt
technical//911report/chapter-13.2.txt
technical//911report/chapter-13.3.txt
technical//911report/chapter-3.txt
technical//911report/chapter-2.txt
technical//911report/chapter-1.txt
technical//911report/chapter-5.txt
technical//911report/chapter-6.txt
technical//911report/chapter-7.txt
technical//911report/chapter-9.txt
technical//911report/chapter-8.txt
technical//911report/chapter-12.txt
technical//911report/chapter-10.txt
technical//911report/chapter-11.txt
zac@Zacs-MacBook-Pro docsearch % 
```
>Explanation:

## Command 2 - find -maxdepth

Example 1: find technical -maxdepth 1 -type d

Source: [https://man7.org/linux/man-pages/man1/find.1.html](https://man7.org/linux/man-pages/man1/find.1.html)
```
zac@Zacs-MacBook-Pro docsearch % find technical -maxdepth 1 -type d
technical
technical/government
technical/plos
technical/biomed
technical/911report
zac@Zacs-MacBook-Pro docsearch % 
```
>Explanation:

Example 2: find technical -maxdepth 2 -type d

Source: [https://man7.org/linux/man-pages/man1/find.1.html](https://man7.org/linux/man-pages/man1/find.1.html)
```
zac@Zacs-MacBook-Pro docsearch % find technical -maxdepth 2 -type d               
technical
technical/government
technical/government/About_LSC
technical/government/Env_Prot_Agen
technical/government/Alcohol_Problems
technical/government/Gen_Account_Office
technical/government/Post_Rate_Comm
technical/government/Media
technical/plos
technical/biomed
technical/911report
zac@Zacs-MacBook-Pro docsearch % 
```
>Explanation:

## Command 3 - find -type

Example 1: find technical -type d

Source: [https://man7.org/linux/man-pages/man1/find.1.html](https://man7.org/linux/man-pages/man1/find.1.html)
```
zac@Zacs-MacBook-Pro docsearch % find technical -type d
technical
technical/government
technical/government/About_LSC
technical/government/Env_Prot_Agen
technical/government/Alcohol_Problems
technical/government/Gen_Account_Office
technical/government/Post_Rate_Comm
technical/government/Media
technical/plos
technical/biomed
technical/911report
zac@Zacs-MacBook-Pro docsearch % 
```
>Explanation:

Example 2: find technical/911report -type f

Source: [https://man7.org/linux/man-pages/man1/find.1.html](https://man7.org/linux/man-pages/man1/find.1.html)
```
zac@Zacs-MacBook-Pro docsearch % find technical/911report -type f
technical/911report/chapter-13.4.txt
technical/911report/chapter-13.5.txt
technical/911report/chapter-13.1.txt
technical/911report/chapter-13.2.txt
technical/911report/chapter-13.3.txt
technical/911report/chapter-3.txt
technical/911report/chapter-2.txt
technical/911report/chapter-1.txt
technical/911report/chapter-5.txt
technical/911report/chapter-6.txt
technical/911report/chapter-7.txt
technical/911report/chapter-9.txt
technical/911report/chapter-8.txt
technical/911report/preface.txt
technical/911report/chapter-12.txt
technical/911report/chapter-10.txt
technical/911report/chapter-11.txt
zac@Zacs-MacBook-Pro docsearch % 
```
>Explanation:

## Command 4 - find -size

Example 1: find technical -size +250k

Source: [https://man7.org/linux/man-pages/man1/find.1.html](https://man7.org/linux/man-pages/man1/find.1.html)
```
zac@Zacs-MacBook-Pro docsearch % find technical -size +250k
technical/government/Gen_Account_Office/Statements_Feb28-1997_volume.txt
technical/government/Gen_Account_Office/d01591sp.txt
technical/911report/chapter-13.4.txt
technical/911report/chapter-13.5.txt
technical/911report/chapter-3.txt
zac@Zacs-MacBook-Pro docsearch % 
```
>Explanation:

Example 2: find technical -size -1k

Source: [https://man7.org/linux/man-pages/man1/find.1.html](https://man7.org/linux/man-pages/man1/find.1.html)
```
zac@Zacs-MacBook-Pro docsearch % find technical -size -1k
technical
technical/government
technical/government/About_LSC
technical/government/Env_Prot_Agen
technical/government/Alcohol_Problems
technical/government/Post_Rate_Comm
technical/plos/pmed.0020191.txt
technical/plos/pmed.0020226.txt
technical/911report
zac@Zacs-MacBook-Pro docsearch % 
```
>Explanation:

Chose one of the bugs from week 4's lab.

Provide:

A failure-inducing input for the buggy program, as a JUnit test and any associated code (write it as a code block in Markdown)
An input that doesn't induce a failure, as a JUnit test and any associated code (write it as a code block in Markdown)
The symptom, as the output of running the tests (provide it as a screenshot of running JUnit with at least the two inputs above)
The bug, as the before-and-after code change required to fix it (as two code blocks in Markdown)
Briefly describe why the fix addresses the issue.

Consider the commands less, find, and grep. Choose one of them. Online, find 4 interesting command-line options or alternate ways to use the command you chose. To find information about the commands, a simple Web search like “find command-line options” will probably give decent results. There is also a built-in command on many systems called man (short for “manual”) that displays information about commands; you can use man grep, for example, to see a long listing of information about how grep works. Also consider asking ChatGPT!

For example, we saw the -name option for find in class. For each of those options, give 2 examples of using it on files and directories from ./technical. Show each example as a code block that shows the command and its output, and write a sentence or two about what it’s doing and why it’s useful.

That makes 8 total examples, all focused on a single command. There should be two examples each for four different command-line options. Many commands like these have pretty sophisticated behavior possible – it can take years to be exposed to and learn all of the possible tricks and inner workings.

Along with each option/mode you show, cite your source for how you found out about it as a URL or a description of where you found it. See the syllabus on Academic Integrity and how to cite sources like ChatGPT for this class.



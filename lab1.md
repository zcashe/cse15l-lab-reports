
[Index](https://zcashe.github.io/cse15l-lab-reports/index.html)
---
# Lab 1 Report 
---
## Markdown
I have learned how to
* *Do Italics*
*  **BOLD**
*  > Do Blockquotes
List numbers
1. H
2. I
`print(" Do Inline Code")`
---
## Command Line

# Using cd


**No Args**
```
[user@sahara ~]$ cd
```
 Puts user in home directory, doesn't do anything since already in home directory

**Directory**
```
[user@sahara ~]$ cd lecture1/
[user@sahara ~/lecture1]$
```
 Changes Directory to the specified directory

**File**
```
[user@sahara ~/lecture1]$ cd messages/en-us.txt 
bash: cd: messages/en-us.txt: Not a directory
```
Cd only allows us to move to directories not actual files, this produces a error message telling us that the thing we tried to cd into wasn't a directory



# Using ls

**No Args**
```
[user@sahara ~]$ ls
lecture1
```
Shows us the content of the home directory

**Directory**
```
[user@sahara ~]$ ls lecture1/
Hello.class  Hello.java  messages  README
```
This shows us the content within the directory we put as the argument

**File**
```
[user@sahara ~]$ ls lecture1/Hello.class 
lecture1/Hello.class
```
When we ls into a file it just shows us the relative path to the file

# Using cat
---
**No Args**
```
[user@sahara ~]$ cat
hi
hi
test
test
```
Produces empty line and duplicates anything I enter into the command line, I believe this is an error due to trying to cat the root directory. 

**Directory**
```
[user@sahara ~]$ cat lecture1/
cat: lecture1/: Is a directory
```
Tells us that it is a directory so it can't read us anything from it

**File**
```
[user@sahara ~/lecture1]$ cat messages/fr.txt 
Bonjour le monde!
```
It reads us the content from the file we selected

## Final Message 
![Image](assets/dogstare.jpg)
![Image](assets/=P.jpg)


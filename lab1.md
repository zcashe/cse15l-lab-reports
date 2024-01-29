
[Index](https://zcashe.github.io/cse15l-lab-reports/index.html)
---
# Lab 1 Report 
---
## Markdown
I have learned how to
* *Do Italics*
*  **BOLD**


List numbers
1. H
2. I

`print("Do Inline Code")`

---
# Commands In Terminal
## Command Line

### Using cd


**No Args**
Working Directory - /home
```
[user@sahara ~]$ cd 
[user@sahara ~]$ 
```
> Puts user in home directory, doesn't do anything since already in home directory.
> This is not an error

**Directory**
Working Directory - /home
```
[user@sahara ~]$ cd lecture1/
[user@sahara ~/lecture1]$
```
> Changes Directory to the directory specified in the argument, which we can see from the change in prompt.
> This is not an error.

**File**
Working Directory - /home/lecture1
```
[user@sahara ~/lecture1]$ cd messages/en-us.txt 
bash: cd: messages/en-us.txt: Not a directory
```
> Cd only allows us to move to directories not actual files, so this produces a error message telling us that the thing we tried to cd into wasn't a directory.
> This is an error.


### Using ls

**No Args**
Working Directory - /home
```
[user@sahara ~]$ ls
lecture1
```
> Using ls without any arguments shows us the files and folders of our current directory.

**Directory**
Working Directory - /home
```
[user@sahara ~]$ ls lecture1/
Hello.class  Hello.java  messages  README
```
> This shows us the files and folders within the directory we put as the argument.
> This is not an error. 

**File**
Working Directory - /home
```
[user@sahara ~]$ ls lecture1/Hello.class 
lecture1/Hello.class
```
> When we ls into a file it just shows us the relative path to the file from the directory where it was called.
> This is not an error

### Using cat
---
**No Args**
Working Directory - /home
```
[user@sahara ~]$ cat
hi
hi
test
test
```
> Produces empty line and duplicates anything I enter into the command line, I believe this is due to the cat reading the terminal and once we input it, it reads it back out.
> This is not an error 

**Directory**
Working Directory - /home
```
[user@sahara ~]$ cat lecture1/
cat: lecture1/: Is a directory
```
> When we run cat on a directory it produces an error message telling us that it is a directory so it can't read us anything from it.
> This is an error message.

**File**
Working Directory - /home/lecture1
```
[user@sahara ~/lecture1]$ cat messages/fr.txt 
Bonjour le monde!
```
> When we use cat on a file it reads us the content from the file we selected in the argument.
> This is not an error.

## Final Message 
![Image](assets/dogstare.jpg)
![Image](assets/=P.jpg)


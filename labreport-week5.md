# Lab Report - Week 5

The command that I will research for this report is `grep`

**Note**: This command works on Linux (and WSL) but not Command Prompt or Powershell

Three `grep` command-line options that can be useful are

* `-n`
* `-c`
* `-w`

## **Part 1: -n command**

When it comes to using `grep`, the `-n` command is used to get all of the lines that match a pattern and their corresponding line numbers

The below screenshot shows one way how `grep -n` is used, in this case it searches for the keyword "2001" in text files in the subdirectory biomed

**Input**: `grep -n "2001" biomed/*.txt`

![](grep(-n1).png)

You can also use the option when looking through a single file instead of multiple files

**Input**: `grep -n "Air Force" 911report/chapter-10.txt`

![](grep(-n2).png)

Finally, you can use the command to search through files if their path meets a certain structure

**Input**: `grep -n "observation" */ar*.txt`

![](grep(-n3).png)

When you run the `-n` option, it searches through all of the files for the pattern and returns the lines that contains that pattern. This option is useful if you want to get the specific lines where a certain pattern is found.

## **Part 2: -c command**

When you use `grep`, the `-c` command counts the number of lines that match the provided pattern

A basic example is in the screenshot down below

**Input**: `grep -c "Air Force" 911report/*.txt`

![](grep(-c1).png)

You can also use it along with other commands as well, in the screenshot below it is also used with the `-w` option, which is used to get the lines with the **WHOLE** pattern 

**Input**: `grep -c -w "2001" *.txt`

![](grep(-c2).png)

Finally, it works when you want to search through files with a certain structure

**Input**: `grep -c "conference" */*/*.txt`

![](grep(-c3).png)

This command is useful if you want to get the number of occurrences a pattern shows up in certain files. However, if a file does not contain the listed pattern, it would still be returned anyway.

## **Part 3: -w command**

When using `grep`, the `-w` command searches a file or files that contain the whole pattern, not the whole pattern when you run grep normally.

The screenshot down below is a basic use of the `-w` command

**Input**: `grep -w "Air Force" 911report/*.txt`

![](grep(-w1).png)

It also works along with the `-i` option, where you get all the occurrences with the exact listed pattern without considering the case

![](grep(-w2).png)

When using it with the `-B n` option, you would get all of the lines that contain the pattern plus the lines before it

**Input**: `grep -w -B 4 "experiment" biomed/*.txt`

![](grep(-w3).png)

This option is useful if you want to only get the lines that mention the exact pattern instead of being a substring of the pattern.
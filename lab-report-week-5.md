# CSE15L Lab Report Week 5: Researching Commands
In this Lab Report, I am going to show three - commands for 'grep'.
## 1. grep -c
In this section, I am going to show the function of -c command for grep. The -c command prints the number of lines that fits what we are fitting for, instead of printing all target lines which is the default behavior of grep.

For instance, I wrote the result of 'find 911report "*.txt"' into a new file I created "find_911_txt.txt". By using 'grep -c' on the new file, I got the following result:
```
$ find 911report "*.txt"
911report 
911report/chapter-1.txt
911report/chapter-10.txt
911report/chapter-11.txt
911report/chapter-12.txt
911report/chapter-13.1.txt
911report/chapter-13.2.txt
911report/chapter-13.3.txt
911report/chapter-13.4.txt
911report/chapter-13.5.txt
911report/chapter-2.txt
911report/chapter-3.txt
911report/chapter-5.txt
911report/chapter-6.txt
911report/chapter-7.txt
911report/chapter-8.txt
911report/chapter-9.txt
911report/preface.txt
find: ‘*.txt’: No such file or directory

$ find 911report "*.txt" > find_911_txt.txt

$ wc find_911_txt.txt
 18  18 434 find_911_txt.txt

$ grep -c ".txt" find_911_txt.txt
17
```
As shown in the code block above, I first 'find' all files ending with '.txt' in 911report directory. The printed result contains the directory name and 17 .txt paths. I then wrote the result into the new file, and used 'grep -c' to search for lines that contains '.txt'. As expected, the result prints 17 which is exactly the number of lines that contain '.txt' in find_911_txt.txt.

Here are two other examples for 'grep -c':
```
$ grep -c "plane" 911report/chapter-1.txt
71

$ grep "plane" 911report/chapter-1.txt > grep_plane.txt

$ wc grep_plane.txt
   71  5321 32345 grep_plane.txt
```
Since the file chapter-1.txt is in 911report directory, I assumed it would mention 'plane' quite frequently. The 'grep -c' line shows 'plane' is mentioned 71 times in chapter-1.txt. In order to comfirm that, the other two commands first wrote all lines in chapter-1.txt into a new file, then counts the number of lines in that file. Since the file should contain all lines in chapter-1.txt that contain 'plane', and the 'wc' command prints 71, which matches the result of my 'grep -c' line, I am convinced that 'grep -c' is also working in this example.
```
$ find plos "*.txt" > find_plos_txt.txt

$ grep -c ".txt" find_plos_txt.txt
252
```
This time, I found the number of txt files in plos directory. Similar to the second example, the result is too large for counting line by line, hence the 'grep -c' is an efficient method for this purpose. Furthermore, from example 2, we found the combination of 'grep' and 'wc' can accomplish the same goal; however, by using 'grep -c', I only need 1 line command which once again shows the efficency of 'grep -c'.

## 2. grep -v
```
$ grep -v ".txt" find_911_txt.txt
911report

```
'grep -v' is the invert search command for 'grep'. Its search result excludes lines with the key words provided. In this example, the key word is '.txt'. Since find_911_txt.txt is a file full of paths ending with '.txt', the only result returned is the '911report' line. Below are more examples:
```
$ grep -v "plane" 911report/chapter-1.txt > no_plane.txt

$ grep "plane" no_plane.txt

```
The '-v' command for grep is useful if one wants to search for all lines in a file excluding those with certain keywords. For instance, in the previous section, we learned 'chapter-1.txt' in 911report has the word 'plane' occur many times. If we want to delete all lines in 'chapater-1.txt' that contain 'plane' for some reason, the code provided above would done the job. As shown in line 'grep "plane" no_plane.txt', its output is blank; we 'removed' all the lines that contain 'plane'.
```
$ find government/About_LSC > find_government_About_LSC.txt

$ grep -v "report" find_government_About_LSC.txt
government/About_LSC
government/About_LSC/Comments_on_semiannual.txt
government/About_LSC/conference_highlights.txt
government/About_LSC/CONFIG_STANDARDS.txt
government/About_LSC/diversity_priorities.txt
government/About_LSC/LegalServCorp_v_VelazquezDissent.txt
government/About_LSC/LegalServCorp_v_VelazquezOpinion.txt
government/About_LSC/LegalServCorp_v_VelazquezSyllabus.txt
government/About_LSC/ODonnell_et_al_v_LSCdecision.txt
government/About_LSC/ONTARIO_LEGAL_AID_SERIES.txt
government/About_LSC/Protocol_Regarding_Access.txt
government/About_LSC/State_Planning_Report.txt
government/About_LSC/State_Planning_Special_Report.txt

```
In the third example, I imagined someone who is interested in 'LSC', hence decides to read the files in 'About_LSC'. Nevertheless, this someone hates reading 'report', hence someone would like to skip any file that contains 'report' in its name. 'grep -v' can help this someone in such situation. While 'grep -v' does not give someone just the desired file, with the names of files that someone needs, if, say someone has not downloaded the files from the remote server yet, someone can use the information provided by 'grep -v' to download just the files that someone would like to read.

## 3. grep -o
This one is quite interesting because I can't think of a way how it is useful. The command will print the matched parts of a matched line only. Hence, in the example below, the '.txt' line is printed for as many times as it appears in find_911_txt.txt.
```
$ grep -o ".txt" find_911_txt.txt
.txt
.txt
.txt
.txt
.txt
.txt
.txt
.txt
.txt
.txt
.txt
.txt
.txt
.txt
.txt
.txt
.txt

```
As always, commands can make things easier if you are dealing with large amount of lines/data, for instance, the code below prints plane for far more than 17 times(the number of .txt above).
```
$ grep -o "plane" 911report/chapter-1.txt
plane
plane
plane
plane
plane
plane
plane
plane
...
```
Obviously, 'grep -o' achieves to print a key word/ many key words from a file for as many times as it/they appear, but why? I think at this point I have reached both my limitations of imagination and knowledge. Some combination of 'grep -o' and other commands must be very useful, that I believed! Hence this is the last command-line option I chose for this report.

# CSE15L Lab Report Week 7: VIM
## Part1
I decided to recreate these steps which I also used to change all 'start' in DocSearchServer.java to 'base'.

To change the first 'start' in the file to 'base', after opening DocSearchServer.java in vim, I need to press exactly these buttons:

`/start<Enter>dwibase<Exit>
`

The '/start' plus 'enter' command told vim to find 'start' in text. Then, 'dw' is used to delete the word found, while 'i' is for entering vim's insert mode. On the exact location where 'start' was deleted, I typed 'base' as replacement, and finally hit 'exit' to return to normal mode.

There are four 'start' in DocSearchServer.java, hence the above operations need to be repeated four times before exiting vim, so the complete list of buttons will be:
`/start<Enter>dwibase<Exit>/start<Enter>dwibase<Exit>/start<Enter>dwibase<Exit>/start<Enter>dwibase<Exit>:wq`

':wq" in the end is used to save all changes and quit vim.

## Part2 
The first method took me 1 minute and 27 seconds while the second method took 1 minute and 11 seconds.
Since the second method is faster than the first even if I am still not proficient in using vim, I think the second method is better when it comes to time efficiency.

In a project/task, I would first consider the size of the file/directory each time I make a change. For larger file/directory, if tools such as 'git clone' which is much faster than 'scp' are not available, changing the file remotely will be a much perferable method. On the other hand, larger project/task may come with more compliated needs for editing. In my opinion, vim's operation is more abstract hence less manageble than editing tools such as vscode even for those proficient vim users. Therefore, to guarantee the accuracy of the changes, the first method would be preferable. In conclusion, since the scale and complexity of a project are almost synonyms, chasing for time efficiency will always be at cost of accuracy and vice versa, when only given those two methods, I would like two consider which method to use based on the specific requirements for the projecct/task.
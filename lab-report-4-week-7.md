# Lab Report 4 - Week 7
Learning how to use vim!
## Part 1
In lab last week we were given the task to: 
* In `DocSearchServer.java`, change the name of the `start` parameter of `getFiles`, and all of its uses, to instead be called `base`.

For vim this task becomes much easier than searching for code like you normalled would with a mouse and keyboard. 

My group decided that the fastest way to accomplish the tasks with vim was to use the following key presses:
>`/start<Enter>cebase<Esc>n.n.:wq`

`/start<Enter>` 
![Image](week-7-screenshots/step1.png)
Finds occurances of start in our code starting from the top. `/` works as the search command to find things in code, right now we are searching for start. `<Enter>` ends our query after typing `/`.

`ce` 
![Image](week-7-screenshots/ce.png)
`c` stands for change command which will change elements, `e` command taks us to the end of a sequence of characters. `ce` changes characters up to where `e` lands. In this case start gets changed.

`base<Esc>`
![Image](week-7-screenshots/base.png)
The previous `c` command enters us into insert mode so when we type in `base` it acts as if typing it directly into the code. The `<Esc>` takes us out of insert mode.

`n`
![Image](week-7-screenshots/n1.png)
`n` command takes us to the next occurance of where find occurs.

`.`
![Image](week-7-screenshots/period1.png)
The `c` change command gets saved similar to when you copy something on your computer. By pressing `.` you are pasting the previous change you made eariler. By using `n` and `.` we can find all the other cases of `start` in `getFiles` and change them to `base`.
![Image](week-7-screenshots/n2.png)
![Image](week-7-screenshots/period2.png)

`:wq`
![Image](week-7-screenshots/saveandquit.png)
This command servers as a save and quit. `:` allows you to chain commands together in vim. `w` is the save command. `q` is the quit command.

## Part 2
Here I will be testing performing the change above in vscode compared to vim by timing myself. 

It took me 53 seconds to perform the change on **vscode** and run the test on the remote server.

Note: I did have my cs15lfa22 account copied to my clipboard to easily paste into the commandline.

It took me 19 seconds to make the edit in **vim**, exit vim and run the bash script.

-------------------------
I would prefer to use **vim** if I were working on a program that I was running remotely. As seen above there was a huge difference in time that mainly came just from `scp` and `ssh` to copy the local file to remote server and run the file on the remote server. That is a 34 second time difference that can be avoided when performing the same task. Especially on a task like the one I performed that involves changing all occurnaces of a variable name, I would 100% use vim. Changing the variable manually in vscode takes time and could lead to errors in the code if I miss changing a variable name. By using vim I optimize my time and will be able to quickly search for all instances of the variable name so it would be unlikely to miss changing a variable when performing the task.




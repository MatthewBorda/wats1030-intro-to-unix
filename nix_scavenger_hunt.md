# *nix Scavenger Hunt

Complete the following challenges using the command-line interface on your favorite
Unix or Linux operating system. You are welcome and encouraged to consult any
additional documentation online or in books.

Please add your answers/responses/text pastes to the document after each prompt.

Note: For some of the challenges you will need to reference files included with
this repository, so you will need to fork the repo into your own Github account
and then clone it to your development environment.

## The Challenges

### Navigating the Filesystem

* Get an idea of where you are in the operating system. Use the `pwd` command to find your "path to working directory"--your current location in the filesystem of your devbox. *Paste the output of the `pwd` command here:*
  /home/cabox/workspace                                                                                                                                      

* Discover more about this filesystem. Use `ls` (the "list" command)to see what is in this directory. 
  *What directories and files do you see when you run `ls`?*
    The ls command provides the file names
    LICENSE  README.md  challenge_files  nix_scavenger_hunt.md  nix_scavenger_hunt_stretch.md
* You can use *options* to modify how a command runs. Try using `ls -alh` to see the contents of your current directory. 
  *How are the results different when you use the `-alh` options?*
  This adds additional details for the files. The command displays all files and the long format listing 
  
* The `man` ("manual") command tells you more about how any given command works. (*WARNING:* CodeAnywhere does not support the man command. You can click the following link to complete this task: http://linux.die.net/man/)Run `man` to see instructions about how to use `man`. 
Then use `man` to learn what the `a`, `l`, and `h` options mean when used with the `ls` command. *Write down what those options do?*
The -a command lists the directory entries. -l lists the files in a long format and the -h command used with th -l option uses file size suffixes to reduce the number of digits in the file size
* Commands can also take *arguments*, which are usually the names of files or locations that you want the command to work with. Try running `ls /` to see what files are in the *root* directory of the filesystem. *What files and directories do you see listed?*
This is what I see in the root directory
bin   dev  fastboot  lib    media  opt   root  sbin  sys  usr            
boot  etc  home      lib64  mnt    proc  run   srv   tmp  var
* A Unix filesystem has a few special shortcuts to refer to specific locations. `/` indicates the *root* of the filesystem, meaning the top-most directory in the filesystem hierarchy. Use the `cd` ("change directory") command to move to the root directory. (Hint: Use `man` to look up the `cd` command if you have any issues) *Then run `pwd` and paste the output here:*

I set the pwd to the / and get / as the pwd

* Another special shortcut in Unix is the `~` location. This indicates the *user root* directory, meaning the top-most directory in the hierarchy that comes below your user account. Use `cd` to move to `~`. *Run `pwd` and paste the response here:*
I get /home/cabox I had to run the ls to get the workspace directory and then change to the workspace/challenge_files

* Change directory into the `challenge_files` directory. Use `ls` to find only the files with a `.demo` pattern. *How many files do you find?*
I found three with the ls *demo. They were 2015_special_stuff.demo  cloaked-wookie.demo  scooter-double-mamba.demo
* Use the `cd` command to move "up" one directory. *Where are you in the filesystem now?*
/home/cabox/workspace
* Press the up arrow on your keyboard. *What just happened?*
This provides the previous command
* Press the up arrow a few more times. *What do you see?*
This shows more previous committed commands
* Run the `history` command. *What do you see?*
This provides the history of commands committed 
### Observing the System

* Discover what account you are logged into using the `whoami` command. *What username are you currently using?*
It returns "cabox"
* Discover who else is on your system with the `who` command. *Are any other users using your system? If so, list them here:*
This just lists me here: cabox    pts/0        Jan  8 23:44 (54.186.244.104)       
* How long has your system been running? Use `uptime` to see, and *paste the result here:*
It appears I've been up for about 4 hours and is on eastern standard time. 23:45:34 up  4:01,  1 user,  load average: 0.00, 0.00, 0.00 
* Run `ps aux` and review the results. (Hint: Use `man` to learn more about the `ps` command and options.) *How do you interpret what you see here?*
This appears to be the list of all processes, status, and how much resources they consumed. 
* Run `top` and review the results. (Hint: You may need to use `ctrl-c` to get out of this app.) *How do you interpret what you see here?*
This is the top of hte output. PID appears to be the process id. User is the user/owner. It also lists the amount of virual memory used and %CPU and %memory used and total time taken
### Finding and Viewing Files

* Make sure you are in the `challenge_files` directory. Use the `*` wildcard to find all the files that have the word "credit" in the filename. *How many files did you find?*
2
* Use the `more` command to view one of the `credit_cards` files you just discovered. (Hint: Type `q` to quit viewing the file. Press the `spacebar` to page down. Use your keyboard arrows to move up/down.) *What is the date in the file you have viewed?*
The last updated dat is 1/15/2015
* Use the `find` command to search for files more effectively. Search the sub-directories under `challenge_files` to find the location of the file named `modi_laboriosam.txt`. *Where is that file located?*
find -name "modi*" - print
./challenge_files/tmp/modi_laboriosam.txt
* Use the `grep` command to search for text within a file. Use `grep` on all the `.user` files in `challenge_files` to find which files contain "WA" (the abbreviation for Washington state). *How many files did you find?*
grep "WA" *.user                                                    
returned two files: Britt-Erdman.user:O'Harachester, WA 37261                         
Lissie-Strosin.user:Jewessfurt, WA 00816-7241
* Use the `-r` option of `grep` to *recursively* find the text "Waldo" hidden in a file somewhere under the `challenge_files` directory. *Paste the result showing the file and line where the word "Waldo" shows up.*
grep -obr "Waldo" returns 
serial-numbers/eaque_molestiae.txt:551:Waldo

### Pipes and Connecting Commands

* Sometimes it's useful to output the results of a command to a text file for further analysis, reference, or processing. Try running `ls > files.txt`. Notice that the file `files.txt` was created. View that file using `more`. *What do you see in the `files.txt` file?*
This exported the ls output to a new file caled files.txt
* Notice that if you run `ls -alh` in the `challenge_files` directory, the files scroll by very quickly. Sometimes it would be better to get the results in a paginated format. Try running `ls -alh | more`. *Describe what you see when you run `ls -alh | more`.*
It provides the output with the additional data of location, user and size. It also starts at the top of the output so the user can scroll through the list
* Earlier, when you viewed the list of active processes on your devbox using `ps aux`, the list was probably really long. You can make this list more manageable by using the pipe (`|`) to filter the results of `ps` using `grep`. Run `ps aux | grep <your_username>` to see what processes are running for your specific user. *Paste the list of processes that reference your username here:*
I wasn't sure that I was seeing all the records so I output the resuts to a file and pasted from here
ps aux | grep "cabox" > userprocesses.txt
root       556  0.0  0.6  63876  3460 ?        Ss   00:00   0:00 sshd: cabox [priv]  
root       557  0.0  0.6  63876  3460 ?        Ss   00:00   0:00 sshd: cabox [priv]  
root       560  0.0  0.6  63876  3460 ?        Ss   00:00   0:00 sshd: cabox [priv]  
cabox      562  0.0  0.2  63876  1472 ?        S    00:00   0:00 sshd: cabox@pts/0   
cabox      563  0.0  0.2  63876  1472 ?        S    00:00   0:00 sshd: cabox@pts/1   
cabox      564  0.0  0.2  63876  1472 ?        S    00:00   0:00 sshd: cabox@pts/2   
cabox      565  0.0  0.3  18124  2008 pts/0    Ss+  00:00   0:00 -bash
cabox      575  0.0  0.3  18124  2012 pts/1    Ss+  00:00   0:00 -bash
cabox      585  0.0  0.4  18196  2104 pts/2    Ss   00:00   0:00 -bash
cabox      629  0.0  0.2  15520  1148 pts/2    R+   00:19   0:00 ps aux
cabox      630  0.0  0.1   8816   744 pts/2    S+   00:19   0:00 grep --color=auto cabox
# MBiP | Command-line bioinformatics

Over the next two workshops you will have an introduction to command-line bioinformatics. This is more difficult than using online tools but allows you greater control over what you're doing and at scale.

Command-line bioinformatics typically uses a Linux-based operating system, as this is open-source and makes software development easier. Most people and institutions don't have access to a local Linux computer, and therefore cloud computing has become more popular. This is where you connect to a computer virtually, while the physical computer is in a datacentre.

The most common command-line language for Linux is Bash, which we will be using today.

For these workshops, we are going to use Posit Cloud to do this. You may have already used this for R workshops, but it also has terminal access using Bash.

___

#### Getting set-up

1. Log into [Posit Cloud](https://login.posit.cloud/login?redirect=%2Foauth%2Fauthorize%3Fredirect_uri%3Dhttps%253A%252F%252Fposit.cloud%252Flogin%26client_id%3Dposit-cloud%26response_type%3Dcode%26show_auth%3D0%26show_login%3D1)
2. Select 'New Project'
3. Select 'New Project from Git Repository'

GitHub is an online code repository frequently used for software development. You can store code here and easily download it onto a Linux computer using the command-line tool Git.

4. Paste in the following URL for the repository I have set up for the workshop. This will automatically download the material from the repository into the project.

```
https://github.com/Callum-Rimmer/MBiP.git
```
Your screen should now look like this...

![Screenshot](https://user-images.githubusercontent.com/72881801/226890032-f2cd9eec-3639-459e-8e1b-55b0c21ef202.png)

5. Select the 'Terminal' tab at the top. You are now using Bash.

___

#### Basic commands

Let's have a look at some basic commands. The command-line words the same as R, where you need to input commands in order to do something. The difference between R and Bash is the language (called syntax).

###### ls

The `ls` command will list all items in your current directory.

###### pwd

The `pwd` command prints your current working directory to the screen. This is important when you need to supply file paths to files when using software.

###### mkdir

The `mkdir` command allows you create a folder.

###### cd

The `cd` command, change directory, allows you to move between folders.

###### Help

Most commands include an argument (an option) to print a help menu to the screen. This is usually done by writing either `command -help` or `command --help`. This is useful as it will tell you what arguments are available to change the way the command works. It will also tell you whether the command requires an input or not.

Try running both the `pwd` and `mkdir` commands with the help flag on to see the difference.

###### echo

The `echo` command is used to print something to the screen. If you type `echo hello`, the word hello is printed to the screen. This may seem trivial but `echo` can also be used with variables. You will encounter variables later on.

###### cat

The `cat` command is used to print the contents of a file to the screen. Essentially, this is one of the main ways we look at a file using Bash.

`cat` stands for concatenate and can also be used to join multiple files together.

To read a file, type `cat filename`
To join files, type `cat filename1 filename2 filename3 > new_filename`

###### The redirection

In the previous example you will see I used the `>` symbol. This allows you to direct the output of one command into a new file. Have a go at doing this with the ls command, to make a file containing a list of all files in your current directory.

###### touch

The `touch` command allows you to create an empty file. You can do this by typing `touch filename`.

###### rm

The `rm` command is used to delete files or directories.\
To delete a file, type `rm filename`\
To delete an empty directory, type `rm directory_name -d`
To delete a directory containing files, type `rm directory_name -r`

###### cut

The `cut` command allows you to extract specific sections of files.

Let's make a list of letters using the `echo` command, in comma-separated value format (like spreadsheets).
```
echo "a,b,c,d,e" > cut_example.csv
```
Q: How can we print the contents of this file to the terminal?

How do we extract the only the letter C from this file? Using `cut`:
```
cut -f3 -d',' cut_example.csv
```
`-f3` means we are extracting the third field (column).
`-d','` is how we set the delimiter (what the columns are separated by).

So we have broken the file `cut_example.csv` into columns based on commas, then extracted the third column.

###### grep

The `grep` command is a pattern searcher. You supply it with some text and it will seach for that text in whatever file or command output you give it.

Using the file we created in the previous step...
```
grep a cut_example.csv
```
`grep` will output each line that contains a match to your query text.

###### The pipe

The `|` symbol is used to direct the output of one command directly into another command. This is similar to `>`, which directs the output of a command into a new file.

One example of this is counting the number of files in a directory...
```
ls | wc -l
```
`ls` will normally print a list of the contents of a directory to the terminal. If we pipe it into `wc -l` instead (the word count command set to count the number of lines), it will output the number of lines the `ls` command printed i.e. the number of files / directories in your current location.
___

Q: Make a directory called `test`. Move into this folder. Create three different files using the `echo` command. Concatenate these together into a new file. Delete the three original files.
___

##### Package management

Similar to R, there are a variety of programs you can install which perform different analyses etc. The problem is the underlying software requirements for each of these programs can conflict with each other. This is often the case with the version of python you are using. Older programs might still be using python v2 while newer software will use python v3. The required programs for a piece of software are called dependencies, and there is a variety of ways to manage these.

![linux-package-manager-explanation copy](https://user-images.githubusercontent.com/72881801/202696960-655d33be-1e86-46f8-bd0e-c99be19e7609.jpg)

Using a package manager, it will install a program along with its dependencies and place this in an 'environment'. You can have as many environments as you like, each with a different program installed in it. You activate the environment that you wish to use, and you can then use that particular program. This way you will never run into problems with different software conflicting with each other.

##### The package management tool we are going to use is called Conda
\
\
![conda_logo](https://user-images.githubusercontent.com/72881801/202698181-ccb6bbc3-c6c9-4733-9cfe-e47f06001546.png)

1. First we need to download the software. We'll do this using the `wget` command, which allows you to download files from web links. Type...
```
wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh
```
2. You will see that a Miniconda installer has been downloaded. To run it, type...
```
bash Miniconda3-latest-Linux-x86_64.sh
```
3. Press ENTER. The press space to skip to the end of the license agreement. Type yes. When it asks what location to install in, press ENTER.
4. When it asks to initialise Miniconda3 by running conda init, type yes.
5. To switch Conda on now we have installed it, type...
```
source ~/.bashrc
```
Your screen should now look like this:


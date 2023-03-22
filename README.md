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

#### Package management

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

![Screenshot 2023-03-22 at 16 25 05](https://user-images.githubusercontent.com/72881801/226972490-14d7d033-bf42-4d84-b2b9-9f6bbadd1e76.png)

The `base` at the start of the command prompt tells you that we are currently in the base environment for Conda.

6. The last thing to do is update Conda. You can do this by typing...
```
conda update --all
```
#### Creating an environment

The first program we are going to install is called `fastqc`. This program allows you to check the quality of the data from a DNA sequencer.

Before we install the program, we need to create an environment for it...
```
conda create -n fastqc
```
Now we need to turn on this environment...
```
conda activate fastqc
```
We're now in our `fastqc` environment. All we need to do now is install the program. Conda is also used for installing programs, not just managing environments.

Conda installs programs by looking for them in `channels`. To see what `channels` your Conda setup is using, type the command:
```
conda config --show channels
```
We need to add the channel `Bioconda`. This contains most of the programs you need for bioinformatics. To add this channel, type...
```
conda config --add channel bioconda
```
Now we've checked we have the appropriate channels setup, we can install fastqc in our environment by running...
```
conda install fastqc
```
Now fastqc is installed in our fastqc environment. We can check this is installed by typing `conda list`.

Let's check `fastqc` is working by typing `fastqc -h`, if it prints the help page the program is working.

You can turn off your environment by typing `conda deactivate`.

There are a few other conda commands which you need to know...

`conda config --add channels channel_name`          This adds a specific channel if the one you want isn't being used by default

`conda search program_name`                         This searches for a specific program and tells you whether you can install it

`conda info --envs`                                 This prints a list of all your environments

There is a way you can bundle creating an environment and installing a program. Using the example of `fastqc`, you could instead type...
```
conda create -n fastqc fastqc
```
Where the syntax is `conda create -n environment_name program_name`

Another problem you may come across is that some older bioinformatics tools are designed to run on older versions of python. You can specify the version of python an environment is created with by typing...
```
conda create -n environment_name python=python_version
```

## Trying out a small workflow

### Checking the quality of DNA sequencing data

Now that you have an environment setup with fastqc, let's use it.

The GitHub repository you created your R project from contained two DNA sequencing files. The R1 file contains all the DNA sequencing data for the forward reads, R2 contains the data for the reverse reads. [Check out this webpage for more information.](https://www.illumina.com/science/technology/next-generation-sequencing/plan-experiments/paired-end-vs-single-read.html)

Make sure you have activated your fastqc environment.

Make a directory called `raw_reads`. Move the two read files into that directory. What commands do you need to use to do this?

You can run `fastqc` on your read files by typing:
```
fastqc raw_reads/*.fastq.gz
```
Can you answer these questions:

2. What are we saying with `*.fastq.gz`?
3. How would you find out what parameters fastqc needs?


fastqc should output a html file per read file, you can view this using a web browser. You can find out more information about the statistics fastqc outputs by looking at the [project webpage.](https://www.bioinformatics.babraham.ac.uk/projects/fastqc/)

The read quality checks out, so we can move onto the next step.

### Double checking adapter sequences have been removed from our reads

We add adapter sequences to our samples of DNA prior to sequencing so that the DNA binds to the flowcell in the sequencer, as you can see below.

![image](https://user-images.githubusercontent.com/72881801/202675159-54f51a37-45d1-404d-8e68-a2b89bc0e7df.jpeg)

We need to double check that the adapter sequences have been removed before doing any more analysis on the files.

The program we are going to use is called `trimmomatic`.

1. Create an environment called `trimmomatic`
2. Activate this environment
3. Install `trimmomatic`, using conda, in this environment

Trimmomatic uses a few more parameters than fastqc. The command we are going to use is:
```
trimmomatic PE raw_reads/unknown_R1.fastq.gz raw_reads/unknown_R2.fastq.gz -baseout unknown_species_filtered.fastq.gz ILLUMINACLIP:~/miniconda3/envs/trimmomatic/share/trimmomatic-0.39-2/adapters/NexteraPE-PE.fa:2:20:10
```

`unknown_R1.fastq.gz` and `unknown_R2.fastq.gz` are your input files.

`ILLUMINACLIP:~/path/to/NexteraPE-PE.fa:2:20:10` is where the adapter sequences are stored that trimmomatic will look for in your data, along with some extra tweaks to the settings.

The output files are...\
`filtered_reads_1P.fastq.gz` and `filtered_reads_1U.fastq.gz` (paired and unpaired)\
`filtered_reads_2P.fastq.gz` and `filtered_reads_2U.fastq.gz` (paired and unpaired)

The unpaired files can be deleted since they contain all the garbage reads, we just want the paired files.

Now let's tidy things up:

1. Delete the unpaired files if you haven't already.
2. Make a folder called `trimmed_reads` and move your paired files into this folder.

### Assembling the genome

Now our read files have been quality checked and trimmed, we can assemble the reads into a complete genome.

The program we are going to use to do this is called `spades`

1. Create an environment called `spades`
2. Activate the environment and install the program `spades`
```
conda install -c conda-forge -c bioconda spades=3.15.5
```
3. Create a folder called `spades`

Now we can run the main command:
```
spades.py -1 trimmed_reads/filtered_reads_1P.fastq.gz -2 trimmed_reads/filtered_reads_2P.fastq.gz -o spades
```
The `-1` flag is for your trimmed forward reads file.\
The `-2` flag is for your trimmed reverse reads file.\
The `-o` flag is the output folder\

What we're doing is trying to piece the sequencing reads into larger fragments called contigs. The contigs then get stiched together to form the assembled genome.

![image](https://user-images.githubusercontent.com/72881801/202688417-8d9fdf14-2009-4ed4-b17c-0dd48dda76df.png)

Once spades has finished assembling your genome, you will have a `contigs.fasta` file. This file contains all the contigs spades was able to piece the sequence reads into.

Q.  Each contig begins with a header line containing all the information about that contig, starting with a greater than `>` symbol.\
  a)  How can we view this file?\
  b)  How could you extract all the header lines i.e. contig names and print them to the terminal?
  
The below screenshot shows you how to export the `contigs.fasta` file.

![Picture1](https://user-images.githubusercontent.com/72881801/227059669-f72092df-e13e-4e8c-b8e2-1561f9b10192.png)


### Species identification

Now we have our assembled genome, let's find out what species of bacteria it belongs to.

You can upload your fasta file to [PubMLST](https://pubmlst.org/species-id), which uses ribosomal multi-locus sequence typing for species identification.

### Searching for antibiotic resistance genes

We can also upload our genome to the Comprehensive antibiotic-resistance gene database [(CARD)](https://card.mcmaster.ca/analyze/rgi)

Does the genome encode any antibiotic resistance genes?

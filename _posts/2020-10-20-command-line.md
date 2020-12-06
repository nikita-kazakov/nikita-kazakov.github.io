---
title: How to use the Command Line Interface
date: 2020-10-20
layout: post
permalink: /how-to-command-line/
tags: 
    - linux
---

Becoming a software developer forced me to learn the command line interface. At first, I strongly resisted. Coming from windows GUI --- the command line looked like an ugly remnant of 1980s computing.

There's no way around it because you'll need to ssh into your production servers and there won't be a GUI interface. Get comfortable now.

I'll be using `bash` (bourne again shell) --- the most popular shell out there. A lot of this stuff with work wit `zsh` also.

{% include toc %}

# Terminal

To make the transition from GUI interface that you were used to in Windows / MacOS, I recommend you create a folder and put some files in it.

The goal is to learn how to manipulate the files and folders with command line just like you do with your mouse. Here's my setup:
```
└── parent
    ├── folder1
    ├── folder2
    │   └── street-fighter.png
    ├── ryu-image.png
    └── textfile
```

Open up the `parent` directory, right click on it and open the terminal. I'm on MacOS and I like to use iTerm.

```bash
Admins-MacBook-Pro:parent admin$
```

`admin` is me, the user. `$` is the bash prompt symbol. It's the beginning of the command. Instead of prepending the user, I'll simply write $ before each command.

# pwd (print working directory)
Whenever you're lost in the terminal, you can type `pwd` to find your bearings.

```bash
$ pwd
/Users/admin/desktop/parent # this is your working directory.
```

You'll notice that all paths start with `/`. This is the root directory. Everything in Linux is a file (even folders).

# ls (List Directories)

You know your path but you have no idea what files and folders are in that path. `ls` shows you a list of files and folders in your working directory.

```bash
$ ls
folder1		folder2		ryu-image.png	textfile
```

If you have hidden files in your directory ( they start with a `.`), then you'll have to run a `-a` (all) flag to see them.

```bash
$ ls -a

.		.DS_Store	folder1		ryu-image.png
..		.secret-hidden	folder2		textfile
```

For even more info --- go ahead and run the long flag `-l`. It will show you file sizes, permissions, and dates of each file.

```bash
$ ls -l

drwxr-xr-x  2 admin  staff      64 Dec  3 17:47 folder1
drwxr-xr-x  3 admin  staff      96 Dec  3 17:50 folder2
-rw-rw-rw-@ 1 admin  staff  533628 Oct  6 13:17 ryu-image.png
-rw-r--r--@ 1 admin  staff      11 Dec  3 17:48 textfile

```

You'll sometimes see people combine flags together. You can combine `-a` and `-l` into `-al`. Flags will run in the order they are written.

# cd (Change Directory)

You're used to double clicking on a folder to open it. In command line, we'll use the `cd` command.

Let's check which directories are available with the `ls` command and then change a directory with `cd`.

```bash
$ ls
folder1		folder2		ryu-image.png	textfile

$ cd folder2
$ pwd # check if we changed directories.
/Users/admin/desktop/parent/folder2

```

You can navigate using absolute and relative paths. You'll see a starting slash with an absolute path --- for example `/Users/admin/desktop/parent/folder2`.

Let's try to change directories to folder 1.

With an absolute path, we can:

```bash
$ cd /Users/admin/desktop/parent/folder1
```

That's a lot to type. We're already in folder 2. Why not just go up to the parent folder and then change directory to folder1 from there?
```bash
$ cd .. # double dots go up to the parent folder
$ cd folder1 # this is an absolute path
```

Even shorter, we could make that a one-liner:
```bash
$ cd ../folder1
```

Here are some more helpful ways of navigating with `cd`.

```bash
$ cd .  # current directory
$ cd .. # up by one directory (parent)
$ cd ~  # home directory (/home/admin)
$ cd -  # previous directory
```

# Touch

You can even create files in command line using `touch`. It's also used for modifying file timestamps. Each time a file is *touched* a file stamp is updated with the current time.

```bash
$ touch i_made_this
```

Notice that the new file `i_made_this` doesn't even have an extension. Linux doesn't care.

# mkdir (make directory)

We can make files and using `mkdir`, we can make directories.

```bash
$ mkdir new-folder
$ mkdir -p directory/sub/subagain # create nested subdirectories with -p flag.
```

# file

In windows, you can check the properties of a file. You can do that in command line too using `file`.
```bash
$ file ryu-image.png
PNG image data, 780 x 1062, 8-bit/color RGBA, non-interlaced
```

# man (manual)

You don't have to memorize all of these commands. If you ever forget what flags you can set on something, use `man` (manual) to read about each command. To exit, press q.

```bash
$ man file # see the manual on the file command.
$ help file # sometimes this works too.
```

# less

This is a simple command to view text files. I don't prefer it but it does exist. Use vim or nano instead to parse through text files.

# history

If you want to see the history of what you've entered into the command line, this is your friend. Also, press up and down in the command line to scroll through history.

```bash
$ history
```

# clear

Clears your command line terminal.

# cp (copy)

When you need to copy a file, this is your friend.

```bash
# $ cp [file-name] [location]
$ cp textfile folder2 # Let's copy the text file to folder2.
$ cp textfile /Users/admin/Desktop # Use absolute paths if needed.
$ cd folder2
$ ls folder2
# street-fighter.png	textfile
```

There's a lot more you can do with copying. See `man cp` for more features and flags.

Let's try to copy folder2 with multiple files to another folder1. You need to add a `-r` (recursive) to copy all the files and folders within folder2.

```bash
$ cp folder2 folder1 # This won't work. folder2 is a directory (not copied).
$ cp -r folder2 folder1 # This works. -r (Recursive)

```

## wildcards

You can also use wildcards when copying files. Let's say you want to copy all png files.

```bash
$ cp *.png folder2
```

# mv (move)

Let's move some files around.

```bash
$ mv *.png png-images # move all png images to the png-images folder
$ mv file1 file2 new-folder # move multiple files to new-folder.
```

# rm (remove)

This remove (deletes) files / directories. Be careful, once you remove a file, it's gone. There's no recycling bin.

```bash
$ rm textfile # removes text file.
$ rm folder1 # won't remove it as it has subfolders and files.
$ rm -r folder1 # will remove folder1 and all subfolders and files.
$ rmdir folder1 # specially made for removing folders. I'd rather use rm -r.
```

# find

You need a way to search for a file.

```bash
$ find . -name sawyer.txt # Find sawyer.txt in the current directory and it's subdirectories. 
$ find . -name *.png # Find all png file names in the current directory and subdirectories.
```

The above will search for files and folders. Use `man find` to see more options.

# alias 

Want to make your own shortcut for a command? Use `alias`

```bash
$ alias properties='ls -al'
$ properties # will show detailed properties.
$ unalias properties # removes alias.
```

Aliasing is powerful. This is especially useful when you're ssh'ing into a server and need a quick command. Your aliases will not get saved when you exit out of the terminal. If you want to save them, save them to the file `~/.bashrc`.

# exit

```bash
$ exit # quits terminal.
$ logout # logs the user out.
```

You could also just close the terminal window.
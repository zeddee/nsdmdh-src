---
title: "Productive Macos: Lesson 1"
date: 2017-12-07T19:53:37+08:00
draft: true
categories: [productive-macos]
tags: [technical,macos,unix,command,terminal,osx]
---

# Productive macOS

macOS is a powerful operating system that's usually reduced to being described as the shiny veneer that you're paying the Apple tax for. Yes, the Apple tax is real, and bits like [root-gate](https://9to5mac.com/2017/11/28/how-to-set-root-password/) don't make the shiny bits shinier. But the tax is not just for the shine; there is a solid a software and hardware ecosystem that's been tailored to work well together.

This short series will teach you how to make better use of the non-shiny bits of your mac. As long as it runs macOS, this series should cover it.

## The terminal

The terminal is the macOS command-line. You type text into the application window, and your mac does something. Using the command-line when you have a GUI that you can use seems to rather miss the point. But I promise it's worth it.

I use the terminal because:

1. **There's less room for error.** I can get away with horrendous things on the GUI. If I click on a button and it doesn't seem to respond, I click it again. The button might have run my request once, or twice. If I were making a payment, I'd have to hope that whoever designed the payment button took into account that someone might accidentally click their button twice. In the command-line, you have to type exactly what you want, and run it.
2. **Errors are obvious.** If a command fails, the terminal tells me immediately. If the error message is specific enough (which it usually is), I know where to find my answers (i.e. Google).
3. **If you can do it once, you can do it again. And again.** Press the up arrow in the terminal to bring up the last command you ran. Press the up arrow again to bring up the command previous to that command, and so on. Need to make a change to 1500 different files? If you can do it for one file, you can write a script to run it on all 1500 files.

## Terminal ground rules

1. **Run only commands that you understand.** Make sure that you know what you're doing. If you don't, ask someone who does.
2. **If something tells you to run a `sudo` command, make _doubly-sure_ you know what you're doing.** `sudo` commands allow access to system level things. Don't use it unless you really need to.
3. **Not sure what a command does? Test it out first.** Make an empty folder and run the commands. Run the commands on a test file. You'll get the hang of it.
4. **Don't be afraid.** Ask questions. If you mess up, there's likely a way to fix it. If a command fails, it likely wouldn't have changed anything.

## Lesson 1: Figuring out where you are

Open the terminal at: Applications > Utilities > Terminal.app
OR
Open Spotlight (`Cmd+Space`) and type `terminal`. The terminal application should turn up. Hit `Enter` to launch it.

!["Open terminal with spotlight"](/img/productivemacos/spotlight-terminal.gif)

When the terminal loads, you'll be face-to-face with the command-line. You're now working in a **shell**.

What's a shell? All you're seeing is a blank screen, some text, and a blinking cursor. The reason why a GUI is always more comfortable is that a GUI always shows you where you are. In a shell, that's not necessarily true, because it's more economical in presenting information to you. It shows you only the things related to the task at hand. But no worries. It's not hard to find out where you are.

Get acquainted with the shell; run[^Type the command into the terminal and press `Enter`.] the following commands:

* `whoami`
* `pwd`
* `ls -la`

`whoami` prints your Unix user name. This is the user name that the underlying operating system uses to identify you. It may or may not be different from the user name that macOS displays on your mac. The difference doesn't matter; usually, only your Unix user name will be used when performing command-line related functions, not the user name displayed by macOS in System Preferences > Users & Groups.

`pwd` prints the current directory the shell is currently in. If you've run it fresh from opening the terminal, it should print your user directory. It should look something like `/Users/<user_name>`. 

`ls -la` lists the contents of the current directory. We're running the command with two options here, prefixed by a `-`. `-l` tells the shell to display the contents of the folder in a list. `-a` tells the shell to display all contents of the folder, including hidden files (like `.dot` files, or hidden files and folders that begin with a dot).

See? Wasn't that hard.

Now, run the following:

1. `mkdir i_made_this`
2. `cd i_made_this`
3. `pwd`

You've done two things: made a new directory named "i_made_this", and moved into it. To move into the previous working directory, run `cd ..`. Run the `pwd` command to figure out where you are.

## I made this

Navigate into the `i_made_this` directory. Run `pwd` to make sure; you should be in a directory that looks like `/Users/<user_name>/i_made_this`.

Now, run `touch touch_me.txt`

List the contents of the directory. You’ll see that there's now an empty text file named `touch_me.txt` in your current directory.

## Echo and Narcissus

The `echo` command prints to the command line whatever you type after it.  Run `echo "hello, you"`. It should print "hello, you" to the shell. It seems kind of silly, but it’s useful (I promise). For now, we're just going to use it to quickly write something to a text file.

Another command we're going to get familiar with is `cat`. It's not related to felines, but rather short for "concatenate". It prints out the contents of all files passed to it. For now, run `cat touch_me.txt`. See anything? Good. `touch_me.txt` is an empty text file, so nothing should show up in the shell.

>**Tip**: When typing a command, you can hit the `Tab` key to get the shell to try and autocomplete a command. For example, type `cat tou` and hit `Tab`. It should insert the file name `touch_me.txt` into the shell. 

>If there is more than one possible autocompletion, the shell either lists all possible commands for you to choose from, or autocompletes it as best as it can. For example, if there are two files in the directory, one named `touch_me.txt` and another named `touch_me_two.txt`, autocomplete will complete your command as `cat touch_me` and leave you to fill in the rest. Hit `Tab` again to see a list of all files that would fit that prefix.

Let's get to the meat of it. Run the following:
 
 1. `echo "something" >> touch_me.txt`
 2. `cat touch_me.txt`

The shell should now print "something".

The double angled-brackets tell the shell to take the results of whatever the command on the left of it produces and append it to a file on the right side of it. Like this: `<command> >> <file>`.

I use this to quickly write notes into a folder. For example, if I have a folder of images that I've downloaded from a particular online article, I'll `cd` into the folder, and run `echo "https://www.example.com/image-source-url" >> source.txt`. Try it and see what happens.

A single angled-bracket `>` also writes text to files, but instead of appending the text, it _overwrites_ the contents of the file with whatever is on the left of the angled-bracket. Try this on `touch_me.txt`:

1. `cat touch_me.txt`
2. `echo "line 2" >> touch_me.txt`
3. `cat touch_me.txt`
4. `echo "line 3" > touch_me.txt`
5. `cat touch_me.txt`

Now let's try something a bit different. Copy the text below:

```
<!-- http://slipsum.com/ -->
The path of the righteous man is beset on all sides by the iniquities of the selfish and the tyranny of evil men. Blessed is he who, in the name of charity and good will, shepherds the weak through the valley of darkness, for he is truly his brother's keeper and the finder of lost children. And I will strike down upon thee with great vengeance and furious anger those who would attempt to poison and destroy My brothers. And you will know My name is the Lord when I lay My vengeance upon thee.
```

Use `echo` to insert it into a text file. Done? Easy?

## Move it

We'll wrap up in a bit, but first we should clean up after ourselves. We should have a number of text files in the `i_made_this` folder. Let's say we want to move it all into a folder named `archive`.

1. `mkdir archive`
2. `ls`
3. See all these files you have to move?
4. `mv *.txt archive`
5. `ls`

You're done!

## Further reading

* You can get help for most commands by running one of the following:
  * `man <command>`, e.g. `man cat`
  * or you could try `<command> --help`. It doesn't work for all commands, and shell would usually tell you and provide you at least some syntax help anyway.

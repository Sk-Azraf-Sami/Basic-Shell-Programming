# Basic-Shell-Programming

## Table of Contents: 
- [Comments](#Comments)
- [Shebang](#shebang)
- [Data Types](#Data-Types)
- [\ is the bash escape character](#is-the-bash-escape-character)
- [Single and Double Quote](#Single-and-Double-Quote)
- [Read command](#Read-command)
- [Command Substitution](#Command-Substitution)
- [Arithmetic Evaluation](#Arithmetic-Evaluation)

  
## [Comments:](#Comments)

**Single-Line Comments (Using `#`):**

```bash
#!/bin/bash

# This is a single-line comment.
# Single-line comments begin with the '#' symbol.
# They are used to add explanatory notes or comments to your code.

echo "Hello, world!"  # This is another single-line comment.

# You can have single-line comments anywhere in your script.
# They can be on their own line or at the end of a line of code.
```

Explanation:
- Single-line comments in shell scripting start with the `#` symbol.
- They are used for adding comments or explanations to your code.
- Anything following the `#` on a line is treated as a comment and is not executed by the shell.
- Single-line comments can be placed on their own lines or at the end of lines with code.

**Multi-Line Comments (Using Here Document):**

```bash
#!/bin/bash

: '
This is a multi-line comment using a here document.
Multi-line comments are not a standard feature of shell scripting,
but you can use a colon (:) followed by single quotes (') to create one.
The comment text goes between the single quotes.
This can span multiple lines.
'

echo "Hello, world!"

# The actual code starts here.
```

Explanation:
- Multi-line comments are not a native feature of shell scripting, so this is a workaround using a colon and single quotes.
- The colon (`:`) is a no-op (no operation) command that does nothing, and the single quotes (`'`) are used to create a block of text.
- Anything between the single quotes is treated as a comment and is not executed.
- This approach allows you to create multi-line comments, but it's not standard, and not all shells may support it.

In practice, single-line comments using `#` are the most commonly used form of comments in shell scripts because they are widely supported and straightforward. The multi-line comment using a here document is less common and less portable but can be useful when you need to comment out larger blocks of code or explanations.

**In a shell script, you can use `<<`** (the here document syntax) to create multi-line comments instead of using `:` (the no-op command) followed by single quotes (`'`). Here's how you can use `<<` for multi-line comments:

```bash
#!/bin/bash

<<COMMENT
This is a multi-line comment using a here document.
You can include as many lines of comments as you need.
The comment text goes between the 'COMMENT' marker and the corresponding 'COMMENT' marker.
This block of text will not be executed.
COMMENT

echo "Hello, world!"

# The actual code starts here.
```

Explanation:
- In this example, the `<<COMMENT` and `COMMENT` markers are used to delimit the multi-line comment block.
- Anything between the `<<COMMENT` and `COMMENT` markers is treated as a comment and is not executed.
- The `COMMENT` marker can be replaced with any unique identifier you choose; it doesn't have to be uppercase or in all caps, but it should match consistently.

Using `<<` for multi-line comments can be a more readable and structured way to add comments to your code when compared to the `:` and single quotes approach. However, it's important to note that this is still not a standard feature of shell scripting, but it's a widely used convention for creating multi-line comments.

## [Shebang](#shebang)
The line `#!/bin/bash` is called a shebang, also known as a hashbang or pound-bang. It is not required for a shell script to run, but it serves an important purpose.

The shebang is used to specify the interpreter that should be used to execute the script. In this case, `#!/bin/bash` indicates that the script should be interpreted and executed using the Bash shell.

If you don't include a shebang line at the beginning of your script, the script will still run, but it will be executed by the default shell of your system. This behavior may vary depending on the operating system and shell environment.

Here are a few key points about the shebang line:

1. **Interpreter Specification**: The shebang line tells the operating system which interpreter should be used to execute the script. Different scripts may use different interpreters, such as `/bin/bash` for Bash scripts, `/bin/python3` for Python scripts, or `/bin/perl` for Perl scripts.

2. **Compatibility**: Including a shebang line is a good practice because it ensures that your script runs with the desired interpreter, making it more portable and avoiding potential compatibility issues.

3. **Executable Permission**: To run a script as an executable (e.g., `./myscript.sh`), you need to give the script file execute permission (`chmod +x myscript.sh`). The shebang line is essential for the system to understand how to execute the script as an independent program.

4. **Cross-Platform**: The shebang line makes it easier to share and distribute scripts because it explicitly specifies the interpreter, making the script self-contained.

In summary, while a shebang line is not strictly required, it is strongly recommended to include one at the beginning of your shell script to ensure proper interpretation and execution, enhance portability, and make it clear which interpreter the script should use.

## [Data Types](#Data-Types)
Shell programming typically deals with a limited set of data types, primarily because the shell itself is designed for managing and manipulating text and running system commands. Here are some of the common data types used in shell programming with examples:

1. **String**: Shell scripts frequently work with strings, which are sequences of characters.

   ```bash
   name="John"
   echo "Hello, $name"
   ```

2. **Integer**: Although shell scripting primarily handles strings, you can perform arithmetic operations on integers.

   ```bash
   x=5
   y=3
   result=$((x + y))
   echo "Result: $result"
   ```

3. **Array**: Shell supports indexed arrays, allowing you to store multiple values in a single variable.

   ```bash
   fruits=("apple" "banana" "cherry")
   echo "First fruit: ${fruits[0]}"
   ```

4. **Associative Array (Bash)**: Bash supports associative arrays, allowing you to create key-value pairs.

   ```bash
   declare -A person
   person["name"]="John"
   person["age"]=30
   echo "Name: ${person["name"]}, Age: ${person["age"]}"
   ```

5. **Boolean**: While shell scripting doesn't have a native boolean data type, you can use numeric values (0 for false, 1 for true) to represent boolean conditions.

   ```bash
   is_true=1
   is_false=0
   ```

6. **File Descriptor**: In addition to standard variables, shell scripting can work with file descriptors for input, output, and error handling.

   ```bash
   # Redirecting output to a file
   echo "Hello, world!" > output.txt
   ```

7. **Command Output**: Shell scripts often store the output of commands in variables.

   ```bash
   current_directory=$(pwd)
   ```

8. **Null/Unset**: Represents an uninitialized or unset variable.

   ```bash
   unset my_var
   ```

These are the most common data types used in shell scripting. Keep in mind that shell scripting languages like Bash are loosely typed, meaning variables can change types, and operations often depend on context. For example, a variable that held a string can be modified to hold an integer without explicit type declarations. However, understanding and adhering to data type conventions can lead to more readable and maintainable code in shell scripts.

## Where I use $ for variable and where not? 
In Bash scripting, you use the `$` symbol to reference the value of a variable. However, there are specific cases where you use `$` and other cases where you don't. Here's a general guideline:

1. **Referencing Variable Values**: When you want to access the value of a variable, you prepend the variable name with `$`. For example:
   
   ```bash
   variable_name="Hello"
   echo $variable_name
   ```

   In this example, `$variable_name` is used to access the value "Hello" stored in the variable.

2. **Assigning Values to Variables**: When you assign a value to a variable, you don't use `$` on the left side of the assignment. For example:

   ```bash
   variable_name="World"
   ```

   Here, `variable_name` is assigned the value "World" without using `$`.

3. **Mathematical Operations**: When performing mathematical operations with variables, you use `$` to access the variable values. For example:

   ```bash
   num1=5
   num2=3
   sum=$((num1 + num2))
   ```

   Here, `$num1` and `$num2` are used to access the values of the variables for addition.

4. **Command Substitution**: When you want to capture the output of a command and store it in a variable, you use `$()` for command substitution. For example:

   ```bash
   current_date=$(date)
   ```

   Here, `$(date)` is used to execute the `date` command and capture its output in the `current_date` variable.

5. **String Manipulation**: When you want to concatenate strings or perform other string operations, you use `$` to reference the variable values. For example:

   ```bash
   first_name="John"
   last_name="Doe"
   full_name="$first_name $last_name"
   ```

   Here, `$first_name` and `$last_name` are used to concatenate the strings into `full_name`.

In summary, you use `$` to reference variable values, whether you're accessing, manipulating, or assigning values to variables. The `$` symbol indicates to Bash that you are working with the contents of a variable. However, you don't use `$` when declaring or assigning values to variables.

## [\ is the bash escape character](#is-the-bash-escape-character)
```bash
$ ls
bash.pdf   bash.ppt  'CSE 3128 - Lab1 Lab1_ Introduction to Swift.pptx'   Lab-02.pdf   lab2shellScripting.txt  'OS Lab 1.pdf'   test.sh  '*try.txt'

$ ls \*try.txt # Using the backslash to escape the asterisk
'*try.txt'

$ ls '*try.txt' # Using single quotes to preserve the literal value of *
'*try.txt'
```
When I mentioned "escape the asterisk in the filename," I was referring to situations where a filename contains a special character like an asterisk (*).
In shell scripting, some characters, such as *, have special meanings and are used as wildcard characters for pattern matching. If you have a file with a special character like * in its name and you want to treat that character as a literal part of the filename (i.e., you don't want the shell to interpret it as a wildcard), you can "escape" it. Escaping means that you use a special character or sequence of characters to tell the shell to treat the following character as a regular character and not as a special character with its usual meaning.
In this case, the backslash tells the shell to treat the * as a regular character and not as a wildcard. This allows you to work with files that have special characters in their names without having those characters interpreted as something else.

## [Single and Double Quote](#Single-and-Double-Quote)

**Using double quotes to show a string of characters will allow any variables in the quotes to be resolved**
```bash
$ var=“test string”
$ newvar=“Value of var is $var”
$ echo $newvar

Value of var is test string
```

**Using single quotes to show a string of characters will not allow variable resolution**
```bash
$ var=’test string’
$ newvar=’Value of var is $var’
$ echo $newvar

Value of var is $var
```

## [Read command](#Read-command)
```bash
#!/bin/bash
roll_number=115
student_name="Azraf Sami"
echo "My roll is $roll_number"
echo "My name is $student_name"

read user_input
echo "You entered => $user_input"
```
**Another Example**
> This will delete specific file.
```bash
#!/bin/bash
echo -n "Enter the file name to delete:"
read file 
echo "Type 'y' to confirm, 'n' to cancel"
rm -i $file
echo "That was your decision!"  
```
`echo -n "Enter the file name to delete:"`<br>
This line uses the echo command to display the message "Enter name of file to delete: " to the terminal. The -n option is used to suppress the newline character, so the cursor remains on the same line, allowing the user to input text on the same line as the prompt.
<br>
`rm -i $file` <br>
This line uses the rm command to attempt to remove (delete) the file specified by the value stored in the $file variable. The -i option stands for "interactive," and it prompts the user for confirmation before actually removing the file. If the user types 'y' (yes), the file is deleted; if the user types 'n' (no), the file is not deleted.

## [Command Substitution](#Command-Substitution)

**Using backtick(``)**
```bash
#!/bin/bash
LIST=`ls`
echo "$LIST"
```
<blockquote>
Output: <br>
bash.pdf <br>
bash.ppt <br>
Lab-02.pdf <br>
lab2shellScripting.txt <br>
OS Lab 1.pdf <br>
test2.sh <br>
test.sh <br>
</blockquote>

```bash
#!/bin/bash
PS1="`pwd`>"
echo $PS1
```
<blockquote>
Output: <br>
/home/sami/00 3-2>
</blockquote>
In the command:

```bash
PS1="`pwd`>"
```

You are configuring the `PS1` (Prompt String 1) environment variable in a Bash shell. This variable controls the format and appearance of your command prompt in the shell.

Here's an explanation of the command step by step:

1. `PS1=`: This part of the command sets the `PS1` environment variable, which determines the primary prompt string for your shell.

2. "`pwd`": Inside the double backticks (`` ` ``), you have a command substitution. The `pwd` command stands for "print working directory," and it is used to display the current directory path.

3. `>`: This is a character (>) that is included as part of the prompt string.

When you set `PS1` to "`pwd`>", it means your shell prompt will display the current working directory followed by a greater-than sign (`>`). This is a common way to customize your shell prompt to show you the current directory in your command line.

So, when you run the command and see `/home/userid/work> _`, it means that you are in the `/home/userid/work` directory, and the `>` character is part of your customized prompt. The underscore (_) represents the cursor position where you can start typing your commands.

Customizing the `PS1` variable allows you to personalize your shell prompt to display information that you find useful while working in the shell.

**Using $(command)**
```bash
#!/bin/bash
LIST=$(ls)
echo $LIST 
```
> Output: bash.pdf bash.ppt Lab-02.pdf lab2shellScripting.txt OS Lab 1.pdf test2.sh test.sh

## [Arithmetic Evaluation](#Arithmetic-Evaluation)

**Using let**
```bash
#!/bin/bash
let X=2*4+5
echo $X

let Y=10*X-6 
echo $Y 
```
**Using $ [expression] or $((expression))**
```bash
#!/bin/bash
echo “$((123+20))”

VALORE=$[123+20]
echo “$[123*$VALORE]”
```

## Expressions
> -d => check if path given is a directory <br>
> -f => check if path given is a file <br>
> -e => check if file name exists <br>
> -r => check if read permission is set for file or directory <br>
> -s => check if a file has a length greater than 0 <br>
> -w => check if write permission is set for a file or directory <br>
> -x => check if execute permission is set for a file or directory <br> 


## Conditional Statements
- Need to have spaces around [ and ] when using them as part of conditional <br>
  statements like if. (keep space like this ==> if`space`[`space`"$var1" = "$var2"`space`] )
- Enclosing the variables $name and $USER in double quotes to handle cases where they might contain spaces or special characters.

```bash
#!/bin/bash
echo -n "Enter your name:"
read name

USER="sami"
ADMIN="admin"

if [ "$name" = "$USER" ]
then
	echo "Hello, $name, you are a general user"
	
elif [ "$name" = "$ADMIN" ]
then
	echo "You are a ADMIN"
	
else
	echo "Username is wrong"
fi 	
```
<br>

**Nested Condition**
```bash
#!/bin/bash

echo -n "Enter your age: "
read age

if [ "$age" -ge 18 ]; then
    echo "You are an adult."

    if [ "$age" -ge 21 ]; then
        echo "You are also eligible to vote and purchase alcohol."
    else
        echo "You are eligible to vote but not eligible to purchase alcohol."
    fi

else
    echo "You are not an adult."
fi
```
<br>

**Another Example**
> Checking if file directory exits or not
```bash
#!/bin/bash 
echo -n "Enter the path:"
read folderPATH 

if cd $folderPATH
then
	echo "Path is $folderPATH and it contains " ;ls

else
	echo "The directory $folderPATH is not exist"
	exit 1

fi
```
**********************************************

```bash
#!/bin/bash
echo -n "Enter Folder Path:"
read folderPATH
if [ -d "$folderPATH" ]
then 
	echo "$folderPATH is exist and it contains"
	ls "$folderPATH"
else
	echo "Folder directory is not exist" 
	exit 1 
fi 
```
Don't use `PATH` as variable name because it will generate error. Instead of using `PATH` as variable name, I use `folderPATH` as variable name. <br>

The `exit 1` statement in the Bash script you provided is used to indicate an error condition and to exit the script with a non-zero exit status. <br>
In Bash and many other programming languages, it is a common practice to use non-zero exit statuses (typically 1 or higher) to indicate that something went wrong or that an error occurred during script execution. By convention, a script with a non-zero exit status suggests that an error condition was encountered.

## Logical operators
> ! => negate (NOT) a logical expression <br>
> -a => logically AND two logical expressions <br>
> -o => logically OR two logical expressions <br>

```bash
#!/bin/bash

echo -n "Enter your age: "
read age

if [ "$age" -ge 18 -a "$age" -lt 65 ]; then
    echo "You are of working age."
elif [ "$age" -ge 65 -o "$age" -lt 18 ]; then
    echo "You are either a senior or a minor."
else
    echo "Invalid age input."
fi
```

> && => logically AND two logical expressions <br>
> || => logically OR two logical expressions

```bash
#!/bin/bash

echo -n "Enter your age: "
read age

if [ "$age" -ge 18 ] && [ "$age" -lt 65 ]; then
    echo "You are of working age."
elif [ "$age" -ge 65 ] || [ "$age" -lt 18 ]; then
    echo "You are either a senior or a minor."
else
    echo "Invalid age input."
fi
```
## Case Statement

```bash
#!/bin/bash

echo "Choose an option:"
echo "1. Say Hello"
echo "2. Say Goodbye"
echo "3. Say Something else"
echo "4. Quit"

read choice

case $choice in
    1)
        echo "Hello!"
        ;;
    2)
        echo "Goodbye!"
        ;;
    3)
        echo "Something else."
        ;;
    4)
        echo "Quitting..."
        exit 0
        ;;
    *)
        echo "Invalid choice."
        ;;
esac
```
<br>

> Find Even or Odd number
```bash
#!/bin/bash
echo -n "Enter a number:"
read num
remainder=$[$num % 2]

case $remainder in 
	0) 
           echo "$num is even number";;
        1)
           echo "$num is odd number";;
        *) 
           echo "$num is invalid input";;   
 esac 
```
<br> 

> Using "if" and "case" together

```bash
#!/bin/bash
echo -n "Enter a number:"
read num

case $num in 
	[0-9]* )
	    if [ $[$num % 2] -eq 0 ]
	    then
	    	echo "$num is a even number" 
	    else
	    	echo "$num is a odd number"
	    fi;;
	
	*) 
	   echo "$num is a invalid input";;
esac
```
## Iteration Statements

### Using For Structure 

```bash
#!/bin/bash
sum=0
for num in 1 2 3 4 5 
	do
	  sum=$[$sum + $num] 
	done
echo $sum
```
<br> 

**Another Example:**
```bash
#!/bin/bash
for name in Sk. Azraf Sami
	do 
	   echo "My name is $name"
	   sleep 1
	 done
```
<br> 

> If the list part is left off, var is set to each parameter passed to the script ( $1, $2, $3,…)
```bash
#!/bin/bash
for var
	do 
	   echo "The value of variable 'var' is $var"
	   sleep 1
	 done
# $ chmod +x test.sh
# $ ./test.sh arg1 arg2

# Output:
# The value of variable 'var' is arg1
# The value of variable 'var' is arg2

```
### C-like for loop
```bash
#!/bin/bash
echo -n "Enter a number:"
read num
sum=0
for((i=1 ; $i <= $num ; i=$i+1))
	do
	  sum=$[$sum+$i]
	done
echo "The sum of the first $num is: $sum"
```
### While Statements

```bash
#!/bin/bash
echo -n "Enter a number:"
read num

sum=0
i=1

while [ $i -le $num ]
	do 
	  sum=$[$sum+$i]
	  i=$[$i+1]
	done

echo "The sum of the first $num is: $sum"
```
## Continue Statements
## Unix / Linux - Special Variables 
Important link: https://www.tutorialspoint.com/unix/unix-special-variables.htm <br> 

**Example-1**
```bash
#!/bin/sh 

# Comment 1: Check if no command line arguments were provided.
if [ $# -eq 0 ]
then
    echo "Usage: $0 ordinary_file"
    exit 1
fi

# Comment 2: Check if more than one command line argument was provided.
if [ $# -gt 1 ]
then
    echo "Usage: $0 ordinary_file"
    exit 1
fi

# Comment 3: Check if the provided argument is a regular file.
if [ -f "$1" ]
then
    filename="$1"
    set `ls -il $filename`
    inode="$1"
    size="$6"
    echo "Name\t| Inode\t| Size"
    echo
    echo "$filename\t| $inode\t| $size"
    exit 0
else
    echo "$0: argument must be an ordinary file"
    exit 1
fi
```
Run this shell: 
```bash
$ chmod +x demo_1  # Make the script executable
$ ./demo_1 sample.txt
```
Output: 
```bash
Name    | Inode  | Size

sample.txt  | <inode_number> | <file_size>
```

The `ls -li` command is used to list information about files and directories in a directory. Here's what each part of the command means:

- `ls`: This is the command to list files and directories.
- `-l`: This is an option for `ls`, which stands for "long format." When used with `-l`, `ls` provides detailed information about files and directories, including permissions, ownership, size, modification date, and more.
- `-i`: This is another option for `ls`, which stands for "inode." When used with `-i`, `ls` displays the inode number of each file or directory. The inode number uniquely identifies a file or directory on a filesystem.

So, `ls -li` combines these two options to list files and directories in long format (`-l`) and display their inode numbers (`-i`).

To get a list of the meanings of positional parameters in a shell script, you can use the `set` command without any arguments. Here's how you can do it:

```bash
#!/bin/bash

# Output the positional parameters
echo "Positional Parameters:"
echo "\$1: $1"
echo "\$2: $2"
echo "\$3: $3"
# ... and so on for other positional parameters

# Use the set command to list all positional parameters
echo "All Positional Parameters:"
set
```

In this script, `$1`, `$2`, `$3`, and so on represent the individual positional parameters, and the `set` command without arguments lists all positional parameters. When you run the script with arguments, you'll see their values in the output. <br> 

**Example-2**
<br>
change the code of Example-1 <br>
• Change1：When the input parameter represent directory, list the directory’s name, inode, size and owner. The result of directory has the same result as file. <br>
• Change2：Show what the parameter represents, file or directory. <br> 
```bash
#!/bin/sh 

if [ $# -eq 0 ]
then
    echo "Usage: $0 ordinary_file_or_directory"
    exit 1
fi

# Check if the provided argument is a regular file or directory.
if [ -e "$1" ]
then
    target="$1"
    if [ -f "$target" ]
    then
        # It's a regular file.
        echo "It's a regular file"
        set `ls -il $target`
        inode="$1"
        size="$6"
        echo "Name\t| Inode\t| Size"
        echo
        echo "$target\t| $inode\t| $size"
    elif [ -d "$target" ]
    then
        # It's a directory.
        echo "It's directory"
        set `ls -il $target`
        inode="$1"
        size="$6"
        owner="$3"
        echo "Name\t| Inode\t| Size\t| Owner"
        echo
        echo "$target\t| $inode\t| $size\t| $owner"
    else
        echo "$0: argument must be an ordinary file or directory"
        exit 1
    fi
else
    echo "$0: argument does not exist"
    exit 1
fi
```


## Real Life Problems: 

**Move same extension files from one folder to another folder**
```bash
#!/bin/bash

source_folder="/home/sami/Downloads"
destination_folder="/home/sami/Downloads/00mhtml"

if [ ! -d $source_folder ]; then 
   echo "Source folder does not exist!" 
   exit 1 
fi 

if [ ! -d $destination_folder ]; then 
   mkdir -p $destination_folder
fi

sudo mv "$source_folder"/*.mhtml "$destination_folder/"

if [ $? -eq 0 ]; then 
   echo "All files are moved from $source_folder to $destination_folder"

else 
   echo "No mhtml file found in the $source_folder"

fi 
```

In shell scripting, `$?` is a special variable that stores the exit status of the last executed command. It typically holds an integer value, where `0` usually indicates success or that the previous command completed without errors, and a non-zero value indicates some kind of error or failure.

So, when you see `$? -eq 0`, it's a conditional statement that checks if the exit status of the previous command is equal to `0`. If it is, it means the previous command executed successfully, and the condition evaluates to true. If the exit status is not `0`, it means there was an error or failure, and the condition evaluates to false.

Here's a breakdown:

- `$?`: Represents the exit status of the last command.
- `-eq`: This is a comparison operator that checks if two values are equal.
- `0`: The value to which the exit status is compared.

So, `$? -eq 0` essentially means "check if the exit status of the last command is equal to 0," which is a common way to verify if a command completed successfully in a shell script.

⚠️  Some of my mhtml files not move to 00mhtml and they are not exist in source folder either. Where they are gone? <br> 

In your script, you are using the `sudo mv` command to move all files with the `.mhtml` extension from the source folder to the destination folder. However, some of the files might not have been moved for the following reasons:

1. **Permissions:** If some files in the source folder do not have read permissions for the user running the script, the `sudo mv` command won't be able to read and move those files.

2. **File Names:** It's possible that some files in the source folder have special characters or file names that are not supported by the `mv` command. These files might not be moved as expected.

3. **Errors in Source Folder:** There could be errors in the source folder path or the source folder might not contain the expected `.mhtml` files.

To troubleshoot this issue, you can do the following:

1. **Check Permissions:** Verify the permissions of the files in the source folder. You can use the `ls -l` command to list the files and their permissions. Ensure that the user running the script has read permissions for all the `.mhtml` files.

   ```bash
   ls -l /home/sami/Downloads/*.mhtml
   ```

2. **Check File Names:** Check if any of the files in the source folder have special characters or file names that could cause issues with the `mv` command.

3. **Check Source Folder Contents:** Verify that the source folder indeed contains the `.mhtml` files you expect to move. You can use the `ls` command without any filters to list all files in the folder.

   ```bash
   ls /home/sami/Downloads
   ```

4. **Error Handling:** Modify your script to include better error handling and reporting. For example, you can use `rsync` or `cp` instead of `mv` to copy the files and then remove them from the source folder only if the copy was successful. This way, you can avoid losing files.

Here's an example of how you can modify your script using `rsync`:

```bash
#!/bin/bash

source_folder="/home/sami/Downloads"
destination_folder="/home/sami/Downloads/00mhtml"

if [ ! -d "$source_folder" ]; then 
   echo "Source folder does not exist!" 
   exit 1 
fi 

if [ ! -d "$destination_folder" ]; then 
   mkdir -p "$destination_folder"
fi

rsync -a --remove-source-files "$source_folder"/*.mhtml "$destination_folder/"

if [ $? -eq 0 ]; then 
   echo "All files are moved from $source_folder to $destination_folder"
else 
   echo "No mhtml file found in the $source_folder"
fi
```

This modified script uses `rsync` with the `--remove-source-files` option to copy and remove files only if the copy operation was successful. This helps prevent the loss of files during the move operation.



# Basic-Shell-Programming


## Comments:

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

## #!/bin/bash
The line `#!/bin/bash` is called a shebang, also known as a hashbang or pound-bang. It is not required for a shell script to run, but it serves an important purpose.

The shebang is used to specify the interpreter that should be used to execute the script. In this case, `#!/bin/bash` indicates that the script should be interpreted and executed using the Bash shell.

If you don't include a shebang line at the beginning of your script, the script will still run, but it will be executed by the default shell of your system. This behavior may vary depending on the operating system and shell environment.

Here are a few key points about the shebang line:

1. **Interpreter Specification**: The shebang line tells the operating system which interpreter should be used to execute the script. Different scripts may use different interpreters, such as `/bin/bash` for Bash scripts, `/bin/python3` for Python scripts, or `/bin/perl` for Perl scripts.

2. **Compatibility**: Including a shebang line is a good practice because it ensures that your script runs with the desired interpreter, making it more portable and avoiding potential compatibility issues.

3. **Executable Permission**: To run a script as an executable (e.g., `./myscript.sh`), you need to give the script file execute permission (`chmod +x myscript.sh`). The shebang line is essential for the system to understand how to execute the script as an independent program.

4. **Cross-Platform**: The shebang line makes it easier to share and distribute scripts because it explicitly specifies the interpreter, making the script self-contained.

In summary, while a shebang line is not strictly required, it is strongly recommended to include one at the beginning of your shell script to ensure proper interpretation and execution, enhance portability, and make it clear which interpreter the script should use.

## Data Types: 
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

## \ is the bash escape character
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

## Single and Double Quote

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

## Read command

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

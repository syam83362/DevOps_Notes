# Bash Basics

## 1. What is Bash?

**Bash** stands for **Bourne Again SHell**.

Bash is a **command-line shell and scripting language** used to:

- Run commands
- Interact with the Linux operating system
- Automate repetitive tasks
- Write shell scripts

Bash is commonly used on Unix/Linux systems.

Example:

```bash
ls
cd /home
mkdir test
```

These commands can be executed directly in the terminal or placed inside a Bash script.

---

# 2. Bash Environment Variables

Environment variables store information about the current shell/session.

Some commonly used variables are:

```
$HOME
$USER
$PATH
```

---

## $HOME

```bash
echo $HOME
```

`$HOME` contains the path of the **current user's home directory**.

Example:

```
/home/syam
```

So:

```bash
cd $HOME
```

takes you to the current user's home directory.

---

## $USER

```bash
echo $USER
```

`$USER` contains the **current username**.

Example:

```
syam
```

---

## $PATH

```bash
echo $PATH
```

`$PATH` contains a list of directories where the shell looks for **executable commands/programs**.

Example:

```
/usr/local/bin:/usr/bin:/bin
```

When you type:

```bash
python
```

Bash searches the directories listed in `$PATH` to find the `python` executable.

### Important

`$PATH` does **not** mean commands/executables in the current directory.

It means:

> Directories where the shell searches for executable commands.
> 

---

# 3. printenv

```bash
printenv
```

Shows the environment variables available in the current environment.

You can also check a specific variable:

```bash
printenv HOME
printenv USER
```

Equivalent examples:

```bash
echo $HOME
printenv HOME
```

---

# 4. Bash Variables

Variables allow us to store values.

Example:

```bash
name="syam"
```

Now the variable `name` contains:

```
syam
```

To access the value:

```bash
echo $name
```

Output:

```
syam
```

### Important: No spaces around `=`

Correct:

```bash
name="syam"
```

Incorrect:

```bash
name = "syam"
```

Bash treats spaces differently, so variable assignment must not have spaces around `=`.

### Basic pattern

```
variable="value"
```

Then:

```
$variable
```

is used to access the value.

---

# 5. Command-Line Arguments

Arguments allow us to pass values to a script when running it.

Example script:

```bash
#!/bin/bash

echo "Hello $1"
```

Save it as:

```
test.sh
```

Run:

```bash
sh test.sh syam
```

Output:

```
Hello syam
```

Here:

```
$1
```

means the **first command-line argument**.

So:

```bash
sh test.sh syam
```

can be understood as:

```
Script → test.sh
$1     → syam
```

---

## Multiple Arguments

Example:

```bash
#!/bin/bash

echo "First: $1"
echo "Second: $2"
```

Run:

```bash
sh test.sh syam manohar
```

Output:

```
First: syam
Second: manohar
```

Common argument variables:

```
$1 → First argument
$2 → Second argument
$3 → Third argument
```

---

# 6. Shebang — #!/bin/bash

At the beginning of a Bash script we commonly write:

```bash
#!/bin/bash
```

This is called a **shebang**.

It tells the operating system which interpreter should be used to execute the script when the script is run directly.

Example:

```bash
#!/bin/bash

echo "Hello DevOps"
```

### Running the script

You can run it through Bash:

```bash
bash test.sh
```

Or make it executable:

```bash
chmod +x test.sh
```

Then:

```bash
./test.sh
```

---

# 7. Conditions — if

Conditions allow a script to make decisions.

Basic structure:

```bash
if [ condition ]; then
    command
fi
```

Example:

```bash
#!/bin/bash

if [ "$USER" = "syam" ]; then
    echo "Welcome Syam"
fi
```

If the current user is `syam`, it prints:

```
Welcome Syam
```

---

## Important: Spaces in `[ ]`

Be careful with spaces.

Correct:

```bash
if [ "$USER" = "syam" ]; then
```

Incorrect:

```bash
if ["$USER"="syam"]; then
```

In Bash, `[ ]` is actually a command (`test`), so the spaces are important.

---

# 8. if / else

We can use `else` when there are two possible outcomes.

Example:

```bash
#!/bin/bash

if [ "$USER" = "syam" ]; then
    echo "You are Syam"
else
    echo "You are not Syam"
fi
```

Flow:

```
           Condition
               ↓
        Is USER = syam?
          ↙          ↘
        YES           NO
         ↓             ↓
   You are Syam   You are not Syam
```

---

# 9. Loops

Loops allow us to execute the same block of code multiple times.

Two common Bash loops are:

```
for
while
```

---

# 10. for Loop

A `for` loop is useful when we want to iterate over a list of values.

Example:

```bash
#!/bin/bash

for name in syam manohar rahul
do
    echo "Hello $name"
done
```

Output:

```
Hello syam
Hello manohar
Hello rahul
```

### How it works

The loop takes each value one by one:

```
name = syam
name = manohar
name = rahul
```

and executes:

```bash
echo "Hello $name"
```

for each value.

---

# 11. while Loop

A `while` loop keeps running **as long as the condition is true**.

Example:

```bash
#!/bin/bash

count=1

while [ $count -le 5 ]
do
    echo "Count: $count"
    count=$((count + 1))
done
```

Output:

```
Count: 1
Count: 2
Count: 3
Count: 4
Count: 5
```

### How it works

Initially:

```
count = 1
```

Condition:

```
count <= 5
```

After every loop:

```bash
count=$((count + 1))
```

increases the value by 1.

Flow:

```
count = 1
   ↓
count <= 5?
   ↓
YES → print count
   ↓
count + 1
   ↓
check again
   ↓
...
   ↓
count = 6
   ↓
NO
   ↓
Exit loop
```

---

# 12. Functions

Functions allow us to group commands into a reusable block.

Example:

```bash
#!/bin/bash

hello() {
    echo "Hello DevOps"
}

hello
hello
```

Output:

```
Hello DevOps
Hello DevOps
```

The function is defined once:

```bash
hello() {
    echo "Hello DevOps"
}
```

Then we can call it multiple times:

```bash
hello
hello
```

---

# 13. Function with a Different Message

Example:

```bash
#!/bin/bash

hello() {
    echo "Syam Sundar"
}

hello
hello
```

Output:

```
Syam Sundar
Syam Sundar
```

---

# 14. Function with Arguments

Functions can also accept arguments.

Example:

```bash
#!/bin/bash

hello() {
    echo "Hello $1"
}

hello Syam
hello Manohar
```

Output:

```
Hello Syam
Hello Manohar
```

Here:

```
$1 → First argument passed to the function
```

---

# 15. Bash Quick Revision

## Bash

```
Bash
→ Command-line shell
→ Scripting language
→ Used for Linux commands and automation
```

## Environment Variables

```
$HOME → Current user's home directory
$USER → Current username
$PATH → Directories searched for executables
```

## Environment

```bash
printenv
```

→ Shows environment variables.

## Variables

```bash
name="syam"
echo $name
```

Remember:

```
No spaces around =
```

## Arguments

```
$1 → First argument
$2 → Second argument
$3 → Third argument
```

Example:

```bash
sh test.sh syam
```

```
$1 = syam
```

## Shebang

```bash
#!/bin/bash
```

→ Specifies Bash as the script interpreter when the script is executed directly.

## Conditions

```bash
if [ condition ]; then
    command
else
    command
fi
```

## Loops

```
for
→ Iterate over a list

while
→ Repeat while a condition is true
```

## Functions

```bash
hello() {
    echo "Hello"
}

hello
```

→ Define once, reuse multiple times.

---

# Bash Commands to Remember

```bash
echo $HOME
echo $USER
echo $PATH

printenv

bash test.sh
sh test.sh syam

chmod +x test.sh
./test.sh
```

### Simple Bash Mental Model

```
Bash
 │
 ├── Commands
 │
 ├── Variables
 │     ├── $HOME
 │     ├── $USER
 │     └── $PATH
 │
 ├── Arguments
 │     ├── $1
 │     ├── $2
 │     └── $3
 │
 ├── Conditions
 │     └── if / else
 │
 ├── Loops
 │     ├── for
 │     └── while
 │
 └── Functions
       └── Reusable code
```

# Tasker

A simple task sheet script written in bash. It uses a csv file located in `~/.tasker/tasks.csv`.

## Usage

```
    Tasker: Create and list tasks
        Syntax: tasker [-l|h] [-t "title"] [-c "content"] [-d "delete"]

    Options:
        l                   List tasks
        d                   Delete a task.
        t "title"           Title of new task.
        c "content"         Content for new task.
        h                   Print this text.

```

The `-l` flag just echoes into the terminal, so you can use chad pipes to do what you want with the output.

Output example:

```bash
>>> tasker -l
1) Task1: TaskContent

# Using pipes
>>> tasker -l | dmenu -l 10 -p "Which task"
```

The `-d` flag behaves similarly.

```bash
>>> tasker -d
1) Task1: TaskContent

Delete Which? (Task Name):
Select Name: Task1

# OR

echo "Task1" | tasker -d

# OR like how I have in 'dmenu_tasker'

tasks=$(tasker -l | dmenu -p "Tasker (Type 'new' for new task):" -l 5)
echo $tasks | awk '{print $2, $3}' | sed -e "s/: /,/g" | tasker -d
```

## Creating Tasks

When creating tasks, both `-t` AND `-c` are required.

Example:

```bash
>>> tasker -t Title -c Content

# In a script
title="Title"
content="Content"
echo "$title,$content" >> ~/.tasker/tasks.csv

# Without modifying the csv file
title="title"
content="content"
tasker -t $title -c $content
```
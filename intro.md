```python
# Import necessary libraries
import ipywidgets as widgets
from IPython.display import display
import subprocess
from datetime import datetime
from zoneinfo import ZoneInfo
```





<style>
body {
    counter-reset: exercise-counter;
}
h3.exercise:before {
    counter-increment: exercise-counter;
    content: "Exercise " counter(exercise-counter) ". ";
}
</style>




# Introduction to Programming with Python

Welcome to Computer Science! 🚀 In this first chapter, we'll dive into the basics of programming using **Python**, a powerful and popular language known for its simple, readable syntax. We'll also use a special graphics library called **`pytamaro`** to create interesting visuals right from the start.

### Why These Tools?

* **Python:** It's a fantastic language for beginners because its syntax is close to English, letting you focus on programming concepts rather than complex rules. It's also used by professionals at places like Google, NASA, and Spotify.
* **`pytamaro`:** Learning to code is more fun when you can see your results. This library makes it easy to draw shapes, create images, and learn core programming ideas in a visual way.
* **Jupyter Notebooks:** This interactive environment, which you're looking at right now, lets us mix live code, explanatory text, and images all in one place. It’s the perfect digital workbook for learning and experimenting.

---

## Your First Steps in the Notebook

This document is a **Jupyter Notebook**, and it's made up of individual blocks called **cells**. A cell can contain either text (like this one) or code.

**Working with Code Cells**
To run a code cell, you can either click the "play" button (▶️) that appears to its left or select the cell and press `Ctrl+Enter`. This executes the Python code inside and shows the output directly below. You can click on any code cell to edit its contents.

**Working with Text Cells**
The text you're reading is in a **Markdown cell**. Markdown is a simple way to format text using plain characters. To see the "raw" text, just double-click on a text cell. To render it again, press `Ctrl+Enter`.

Here are a few basic Markdown commands:
* `# Title` creates a main heading, `## Subtitle` creates a smaller one.
* `*text*` makes text *italic*.
* `**text**` makes text **bold**.
* `` `code` `` formats text as `inline code`.

---

## Goals for this Chapter

By the end of this chapter, you will be able to:
* Understand the roles of Python, `pytamaro`, and Jupyter Notebooks.
* Confidently navigate and interact with notebook cells.
* Write and execute basic Python commands to create simple graphics.

Let's get started!

## First Steps with PyTamaro




```python

```


```python
2+2
```




    4




```python
for i in range(4):
    print(i)
```

    0
    1
    2
    3



```python
from pytamaro import rectangle, blue, show_graphic

height = 300

# create a white rectangle with the given height and a width 3/2 times larger
background = rectangle(3/2*height, height, blue)

show_graphic(background)  # this shows your background
```


    
![png](intro_files/intro_6_0.png)
    



```python
# Click this button to commit and push all your changes
def git_push_button_clicked(b):
    try:
        timezone = ZoneInfo('Europe/Zurich')
    except Exception as e:
        print(f"Error setting timezone: {e}. Defaulting to system time.")
        now = datetime.now()
    else:
        now = datetime.now(timezone)
    timestamp = now.strftime("%Y-%m-%d %H:%M:%S")
    commit_message=f"Submission at {timestamp}"
    try: 
        subprocess.run(['python','-m','nbconvert','--to','markdown','intro.ipynb'],check=True, capture_output=True, text=True)
        print('saved markdown')
    except subprocess.CalledProcessError as e:
        print('An error occurred while saving as markdown')
        print(e.stderr)
    try:
        # Add all changes
        subprocess.run(['git', 'add', '.'], check=True, capture_output=True, text=True)
        print("Staged all changes.")

        # Commit changes
        subprocess.run(['git', 'commit', '-m', commit_message], check=True, capture_output=True, text=True)
        print("Committed changes.")

        # Push to the remote repository (assuming 'origin' and 'main' or 'master' branch)
        subprocess.run(['git', 'push', 'origin', 'main'], check=True, capture_output=True, text=True)
        print("Pushed to remote repository.")

        print("Git commit and push successful!")
    except subprocess.CalledProcessError as e:
        print("An error occurred during git commands:")
        print(e.stderr)

push_button = widgets.Button(description="Commit & Push")
push_button.on_click(git_push_button_clicked)
display(push_button)
```


    Button(description='Commit & Push', style=ButtonStyle())


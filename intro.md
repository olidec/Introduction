# Introduction

Welcome to 


```python
# Import necessary libraries
import ipywidgets as widgets
from IPython.display import display
import subprocess
from datetime import datetime
from zoneinfo import ZoneInfo
```

## First Steps in Coding

For reasons no one really understands, the first code one writes in a new programming language the first code you write is usually 'Hello World'. In Python the code for that is `print('Hello World')`. This outputs the text 'Hello World' to the standard output.


```python
print("Hello World")
```

    Hello World


This is some new text


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


    
![png](intro_files/intro_7_0.png)
    



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


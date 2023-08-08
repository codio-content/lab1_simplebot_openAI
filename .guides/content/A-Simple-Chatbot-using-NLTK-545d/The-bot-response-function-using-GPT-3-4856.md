At this point, you must be familiar with OpenAI GPT-3 Toolkit. We are going to interact with our prompt to create a response. How we are going to interact with it is by changing our `get_bot_response` function. 

|||info
## Writing Code

To your left, you should see an opened file called `test.py` 
Use this file as demo before we change our code .
|||


Let's see how we can use `openai.Completion.create` to change our simple bot!



In the top left panel, the code file should have the same code as library as we are used to when interacting with GPT-3.
```python-hide-clipboard
import os
import openai
openai.api_key=os.getenv('OPENAI_KEY')
```
Now we are going to create a function `get_bot_response`.The function `get_bot_response(user_input)` generates a bot response by sending a user's input to the OpenAI GPT-3 model, "text-davinci-002", and returns the model's generated text as the bot's response, stripped of leading and trailing whitespace.
```python

# Generating response
def get_bot_response(user_input):
    prompt = f"Please provide a response to the following user input: '{user_input}'"

    response = openai.Completion.create(model="text-davinci-002",
        prompt=prompt,
        max_tokens=150,
        n=1,
        stop=None,
        temperature=0.5,
    )

    bot_response = response.choices[0].text.strip()
    return bot_response

```
{Try it!}(python3 test.py)

After making sure our code runs without errors we are ready to put it in our main code.  Please make sure to copy everything in `test.py` and paste it after `from tkinter import *` in our `simplebot.py` (bottom left panel). Also make sure to delete our old `get_bot_response` function. 

To run our code and try it: please click the button below. Use the other tab in the bottom-left panel

{Run Chatbot|terminal}(python3 simplebot.py)
<details>
<summary>Code</summary>
Your code should look like this:


```python
import tkinter.scrolledtext as tks #creates a scrollable text window
import os
import openai

openai.api_key=os.getenv('OPENAI_KEY')

from datetime import datetime
from tkinter import *

# Generating response
def get_bot_response(user_input):
    prompt = f"Please provide a response to the following user input: '{user_input}'"

    response = openai.Completion.create(model="text-davinci-002",
        prompt=prompt,
        max_tokens=150,
        n=1,
        stop=None,
        temperature=0.5,
    )

    bot_response = response.choices[0].text.strip()
    return bot_response




def create_and_insert_user_frame(user_input):
  userFrame = Frame(chatWindow, bg="#d0ffff")
  Label(
      userFrame,
      text=user_input,
      font=("Arial", 11),
      bg="#d0ffff").grid(row=0, column=0, sticky="w", padx=5, pady=5)
  Label(
      userFrame,
      text=datetime.now().strftime("%H:%M"),
      font=("Arial", 7),
      bg="#d0ffff"
  ).grid(row=1, column=0, sticky="w")

  chatWindow.insert('end', '\n ', 'tag-right')
  chatWindow.window_create('end', window=userFrame)


def create_and_insert_bot_frame(bot_response):
  botFrame = Frame(chatWindow, bg="#ffffd0")
  Label(
      botFrame,
      text=bot_response,
      font=("Arial", 11),
      bg="#ffffd0",
      wraplength=400,
      justify='left'
  ).grid(row=0, column=0, sticky="w", padx=5, pady=5)
  Label(
      botFrame,
      text=datetime.now().strftime("%H:%M"),
      font=("Arial", 7),
      bg="#ffffd0"
  ).grid(row=1, column=0, sticky="w")

  chatWindow.insert('end', '\n ', 'tag-left')
  chatWindow.window_create('end', window=botFrame)
  chatWindow.insert(END, "\n\n" + "")




def send(event):
    chatWindow.config(state=NORMAL)

    user_input = userEntryBox.get("1.0",'end-2c')
    user_input_lc = user_input.lower()
    bot_response = get_bot_response(user_input_lc) 

    create_and_insert_user_frame(user_input)
    create_and_insert_bot_frame(bot_response)

    chatWindow.config(state=DISABLED)
    userEntryBox.delete("1.0","end")
    chatWindow.see('end')



baseWindow = Tk()
baseWindow.title("The Simple Bot")
baseWindow.geometry("500x250")

chatWindow = tks.ScrolledText(baseWindow, font="Arial")
chatWindow.tag_configure('tag-left', justify='left')
chatWindow.tag_configure('tag-right', justify='right')
chatWindow.config(state=DISABLED)

sendButton = Button(
    baseWindow,
    font=("Verdana", 12, 'bold'),
    text="Send",
    bg="#fd94b4",
    activebackground="#ff467e",
    fg='#ffffff',
    command=send)
sendButton.bind("<Button-1>", send)
baseWindow.bind('<Return>', send)

userEntryBox = Text(baseWindow, bd=1, bg="white", width=38, font="Arial")

chatWindow.place(x=1, y=1, height=200, width=500)
userEntryBox.place(x=3, y=202, height=27)
sendButton.place(x=430, y=200)

baseWindow.mainloop()        
```
</details><br>

And that's it! We've built our first chatbot using GPT-3! Let's run it and interact with it!



{Check It!|assessment}(multiple-choice-3460607931)





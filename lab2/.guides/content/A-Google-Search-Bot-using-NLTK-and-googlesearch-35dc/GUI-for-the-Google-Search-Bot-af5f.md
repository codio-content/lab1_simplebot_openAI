---
Let's build our own Google Search Bot! It will:
- Take user input and use it to run a Google search
- Fetch the text from the top search result
- Using NLP, return the most similar sentence from that text

---
|||info
## chatbot_gui.py
We'll be using the same functions we used in The Simple Bot for the `tkinter` GUI and keep them in a separate file called `chatbot_gui.py`. 
You should be able to see that file in the top left pane going forward. 

|||

(Click on the object/function description to see it highlighted in the code file)
- `baseWindow` - [the main GUI window that contains everything](open_file nlp-apibot/chatbot_gui.py panel=0 ref="baseWindow" count=3)
- `chatWindow` - [displays the conversation between a user and the chatbot](open_file nlp-apibot/chatbot_gui.py panel=0 ref="tks.ScrolledText" count=4)
- `userEntryBox` - [for the user to type their queries for the Chatbot](open_file nlp-apibot/chatbot_gui.py panel=0 ref="#text box for user entry" count=2)
- `sendButton` - [a button that sends the user query to the Chatbot](open_file nlp-apibot/chatbot_gui.py panel=0 ref="sendButton" count=10)
- `send()` - [collects the user input from the userEntryBox, gets the bot_response](open_file nlp-apibot/chatbot_gui.py panel=0 ref="def send" count=12)
- `create_and_insert_user_frame()` - [inserts the user_input into the chatWindow](open_file nlp-apibot/chatbot_gui.py panel=0 ref="create_and_insert_user_frame" count=16)
- `create_and_insert_bot_frame()` - [inserts the bot response into the chatWindow](open_file nlp-apibot/chatbot_gui.py panel=0 ref="create_and_insert_bot_frame" count=16)

[Remove Highlighting](open_file nlp-apibot/chatbot_gui.py panel=0)

{Check It!|assessment}(multiple-choice-776249196)

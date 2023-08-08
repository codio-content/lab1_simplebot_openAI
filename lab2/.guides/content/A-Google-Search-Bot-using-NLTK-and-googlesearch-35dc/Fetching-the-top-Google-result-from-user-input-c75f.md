---
Now that we're all set for the GUI, let's start working on the logic for our Chatbot!

To start with, we want to build a corpus for our chatbot for every `user_input` by fetching the top Google search result.

|||info
## Writing Code

To your left, you should see an opened file called `api_bot.py`
Use this file and reference the syntax below to work on this Lab.
|||

Let's import all the Python packages we'll be using in this lab

Paste the following code in the left pane:

```python
import string
import nltk
import requests

from googlesearch import search
from lxml import html
from bs4 import BeautifulSoup
from sklearn.feature_extraction.text import TfidfVectorizer
from sklearn.metrics.pairwise import cosine_similarity
from nltk.stem import WordNetLemmatizer
```

Now, let's write a function called `get_bot_response` that takes in the `user_input`, and returns the `bot_response`

To get the text from the top Google search result:

- Use the `googlesearch` library to run the search with the `user_input`
- With the Python `requests` library, get the webpage of the top search result
- We'll extract the *html* elements by using the `BeautifulSoup` library and the `lxml` *html* parser and generate the text corpus

Paste the following code in the left pane, right under the `import` statements:

```python
# helper function to generate text corpus from html elements
def generate_corpus(all_p_elements):
    corpus = ""
    for p_element in all_p_elements:
        corpus += '\n' + ''.join(p_element.findAll(text = True))
    return corpus


def get_bot_response(user_input):
    # default bot response
    bot_response = "I'm sorry, I don't think I can help you with that :("
    try:
        # use the google search api to fetch top 3 search results
        google_search_results = list(search(user_input, stop=3, pause=1))
        
        # use the requests api to fetch the top result webpage
        webpage = requests.get(google_search_results[0])
        webpage_tree = html.fromstring(webpage.content)
        webpage_soup = BeautifulSoup(webpage.content, "lxml")
        
        # extract all <p> elements from webpage soup object
        all_p_list = webpage_soup.findAll('p')
        
        # generate corpus from all <p> elements
        google_search_corpus = generate_corpus(all_p_list)

    except:
      # return the default response if corpus is empty
      if len(google_search_corpus) == 0:
        return bot_response
```

<details>
<summary>Code</summary>
Your code should look like this:


```python
import string
import nltk
import requests

from googlesearch import search
from lxml import html
from bs4 import BeautifulSoup
from sklearn.feature_extraction.text import TfidfVectorizer
from sklearn.metrics.pairwise import cosine_similarity
from nltk.stem import WordNetLemmatizer


# helper function to generate text corpus from html elements
def generate_corpus(all_p_elements):
    corpus = ""
    for p_element in all_p_elements:
        corpus += '\n' + ''.join(p_element.findAll(text = True))
    return corpus


def get_bot_response(user_input):
    # default bot response
    bot_response = "I'm sorry, I don't think I can help you with that :("
    try:
        # use the google search api to fetch top 3 search results
        google_search_results = list(search(user_input, stop=3, pause=1))
        
        # use the requests api to fetch the top result webpage
        webpage = requests.get(google_search_results[0])
        webpage_tree = html.fromstring(webpage.content)
        webpage_soup = BeautifulSoup(webpage.content, "lxml")
        
        # extract all <p> elements from webpage soup object
        all_p_list = webpage_soup.findAll('p')
        
        # generate corpus from all <p> elements
        google_search_corpus = generate_corpus(all_p_list)

    except:
      # return the default response if corpus is empty
      if len(google_search_corpus) == 0:
        return bot_response
```
</details><br>

And that's it! We've successfully written the logic that gets us the required data!

{Check It!|assessment}(parsons-puzzle-2566371695)

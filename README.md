This script runs inside Google Colab and uses the LiteLLM library to call an OpenAI model (gpt‑4o).
It sets up your API key, defines a helper function to send messages to the model, and then sends a system + user prompt asking for a function that swaps keys and values in a dictionary.

🔍 Line‑by‑line explanation
1. Install LiteLLM
python
!!pip install litellm
The !! syntax is a Colab/Jupyter shortcut to run a shell command.
This installs LiteLLM, a lightweight wrapper for calling many LLM providers.

2. Import modules and load API key
python
import os
from google.colab import userdata
api_key = userdata.get('OPENAI_API_KEY')
os.environ['OPENAI_API_KEY'] = api_key
userdata.get() retrieves a secret stored in Colab (you set it using the key icon).
The key is placed into an environment variable so LiteLLM can automatically read it.

3. Import LiteLLM and typing helpers
python
from litellm import completion
from typing import List, Dict
completion is the function used to call the model.
List and Dict are used for type hints.

5. Define a helper function to call the LLM
python
def generate_response(messages: List[Dict]) -> str:
    """Call LLM to get response"""
    response = completion(
        model="openai/gpt-4o",
        messages=messages,
        max_tokens=1024
    )
    return response.choices[0].message.content
What this does:
Takes a list of messages (system, user, assistant).
Calls the OpenAI model gpt‑4o.
Returns the assistant’s text output.
This mirrors the OpenAI Chat Completions API format.

6. Prepare the conversation
python
messages = [
    {"role": "system", "content": "You are an expert software engineer that prefers functional programming."},
    {"role": "user", "content": "Write a function to swap the keys and values in a dictionary."}
]
The system message sets the model’s persona.
The user message asks for a function.

6. Call the model and print the result
python
response = generate_response(messages)
print(response)
This sends the conversation to the model and prints whatever code or explanation it returns.

🧩 How everything fits together
Install LiteLLM
Load your API key
Define a wrapper function
Build a chat-style prompt
Call the model

Print the generated answer

This is a clean, minimal example of programmatic prompting in Colab.

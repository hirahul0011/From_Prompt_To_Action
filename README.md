# Build Basic AI Agent From Scratch To Convert Prompt To Action
The concept of AI agent is marking a fundamental shift from predictive AI, which performs passive tasks like translating text, to autonomous agents capable of independent problem-solving and task execution. While a standard model requires constant human direction for every step, an agent provides value by figuring out the necessary actions to reach a high-level goal on its own.

In this article, I will show you how to build one basic AI agent to convert prompt in action from scratch using Google’s ADK (Agent Development Kit). This is an open-source framework that makes it easier to create agents, test them, add tools, and even build multi-agent systems.

## What Is an AI Agent? 
In the simplest terms, an AI agent is a complete software application that can think, plan, and take actions to achieve a specific goal on its own. Unlike a standard AI model that simply answers a question or generates a block of text, an agent is an autonomous actor capable of handling complex, multi-step tasks without a human guiding it at every turn.

## Key Concepts:

### 1\. The "Think, Act, Observe" Loop

The defining characteristic of an agent is that it operates in a continuous, cyclical process.

- **Think:** The agent analyzes its mission and devises a multi-step plan.

- **Act:** It uses external **tools** to perform a task, such as querying a database or calling an API.

- **Observe:** It looks at the result of its action (e.g., "the tracking number is ZYX987") and uses that information to decide the next step.

### 2\. The Core Anatomy

To function effectively, an agent is built with four essential "body parts":

- **The Brain (Model):** A reasoning engine (like a Large Language Model) that evaluates options and makes decisions.

- **The Hands (Tools):** Connections to the outside world that allow the agent to move beyond just writing text, such as the ability to send emails or search the web.

- **The Nervous System (Orchestration):** The layer that manages the loop, keeps track of memory (what has already been done), and ensures the agent stays focused on the mission.

- **The Body and Legs (Deployment):** The secure servers and infrastructure that allow the agent to run reliably as a production service.

### 3\. A Shift in Roles

The sources describe a paradigm shift in how software is created. In traditional software, the developer is a **"bricklayer"** who must precisely define every single logical step for the computer. With AI agents, the developer becomes a **"director"**. They set the scene with instructions, select the "cast" of tools and APIs, and provide the necessary context, then allow the autonomous agent to perform the task.

## Prerequisite To Build This Basic AI Agent
- **Python** installed on your computer
- **Any code editor**, such as VS Code
- [**Google ADK**] — Google's open source framework for end to end agent development
- A **Gemini API key**, which is free to generate

**Note**: we will install **Google ADK** in the virtual Environment which we would create our project in

If you have everything ready, let’s build!

## AI Agent From Scratch To Convert Prompt To Action

### Step 1: Create a Project Directory and Virtual Environment

First, open the command prompt, create a directory and move into it:

```bash
>mkdir From_Prompt_to_Action
>cd From_Prompt_to_Action
```

Now create a virtual environment and activate it:

```bash
>python -m venv from_Prompt_to_Action_venv
>from_Prompt_to_Action_venv\Scripts\activate
```

Then open the VS Code editor to start with the next step:

```bash
>code .
```

### Step 2: Install [Google-Agent Development Kit] via command prompt in VS Code Terminal

```bash
>pip install google-adk
```

### Step 3: Create your Agent project with this command in VS Code Terminal

```bash
>adk create from_Prompt_to_Action_agent
```

As we click enter, it would ask us few questions to be answered.

It would ask us Model to be selected out of two options:

```bash
Choose a model for the root agent:
1. gemini-2.5-flash
2. Other models (fill later)
Choose model (1, 2):
```
*You can select gemini-2.5-flash to save some time and switch to the lighter version afterwards when the rate limit on the gemini-2.5-flash is exhausted*

Then it would ask us to select the backend AI:

```bash
1. Google AI
2. Vertex AI
Choose a backend (1, 2):
```
*You can select Google AI, it has worked perfectly for me so far*

Next, it would ask us to enter the Google API Key with a link suggestion where Google API KEY can be created in few steps:

```bash
Don't have API Key? Create one in AI Studio: https://aistudio.google.com/apikey

Enter Google API key:
```
<img width="1282" height="557" alt="image" src="https://github.com/user-attachments/assets/24638cd8-b763-4369-998b-5f95604b8503" />

Once you enter the Google API Key and hit enter, your agent project would be created and you would see a tree like this in your VS Code editor:

<img width="281" height="136" alt="image" src="https://github.com/user-attachments/assets/0c27304a-5f49-4f19-a206-01922def23fe" />

Please note the followings:
- **agent.py** -> This is the main file where your code lives
- **.env** -> This is where your API key goes
- **__pycache__** and **.adk** -> These are tool and environment related files
- **__init__.py"" -> This file declare a directory as a regular Python package and control which modules and functions are exposed to the rest of the project and its users

### Step 4: Test this Default Agent

Open `agent.py`. You will see the default boilerplate code which is in ready to run state.

Now test your agent. Run this command inside the terminal:
```bash
>adk run from_Prompt_to_Action_agent
```

- Ask something simple. If everything works, you should get an answer.
- Now we are all set with the project.

### Step 5: Creation of Prompt to Action Agent

Now, we would replace the default root_agent with one upgraded root_agent where we are giving the clear instruction to use the Google Search for the User queries and would add google_search as a tool.

Our agent.py file would look like this after the change

```bash
from google.adk.agents.llm_agent import Agent
from google.adk.models.google_llm import Gemini
from google.adk.runners import InMemoryRunner
from google.adk.tools import google_search
from google.genai import types

retry_config=types.HttpRetryOptions(
    attempts=5,  # Maximum retry attempts
    exp_base=7,  # Delay multiplier
    initial_delay=1, # Initial delay before first retry (in seconds)
    http_status_codes=[429, 500, 503, 504] # Retry on these HTTP errors
)

root_agent = Agent(
    name="helpful_assistant",
    model=Gemini(
        model="gemini-2.5-flash",
        retry_options=retry_config
    ),
    description="A simple agent that can answer general questions.",
    instruction="You are a helpful assistant. Use Google Search for current info or if unsure.",
    tools=[google_search],
)
```
*The previous root agent was able to answer the general and historical queries but not related with the current affairs or latest update. With our clear instruction to use the google search for the current info or in case of unsurity, we have overcome that barrier and this updated root agent can answer the queries related with current affairs and latest update as well.*

**Note**: To come out of the conversation with agent, please use Ctrl+C command

### Step 6: Use the Web Interface

ADK includes a web UI.

Inside the terminal, run this command:
```bash
>adk web --port 8000
```
*It would give us this link as a response that we click with Ctrl button pressed.*

```bash
+-----------------------------------------------------------------------------+
| ADK Web Server started                                                      |
|                                                                             |
| For local testing, access at http://127.0.0.1:8000.                         |
+-----------------------------------------------------------------------------+
```

Open the link in your browser. Select your agent from the menu.

<img width="1357" height="641" alt="image" src="https://github.com/user-attachments/assets/d26d7ce9-0f5e-4d31-b0ae-9277f8ede117" />

Now you can see:

- The message flow
- Which agent was called
- The steps they executed

This helps a lot when debugging multi-agent systems.

## Conclusion

Hope I was able to explain the creation of the basic AI Agent to convert Prompt into Action in the most simplest way and you are finding this article helpful anc valuable but please feel free to let me know your valuable feedback and suggestion so that I could make my explanation more helpful and valuable to the end user.

Cheers! ;)




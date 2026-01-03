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






<img width="1360" height="635" alt="image" src="https://github.com/user-attachments/assets/742af25a-0e64-4738-9c4f-69d57f2ca2b3" />





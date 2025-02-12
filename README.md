# Elasticsearch Serverless AI Agent

This little command-line tool lets you manage your [Serverless Elasticsearch projects](https://www.elastic.co/guide/en/serverless/current/intro.html) in plain English. It talks to an AI (in this case, OpenAI) to figure out what you mean and call the right functions using LlamaIndex!

### What Does It Do?
- **Create a project**: Spin up a new Serverless Elasticsearch project.
- **Delete a project**: Remove an existing project (yep, it cleans up after you).
- **Get project status**: Check on how your project is doing.
- **Get project details**: Fetch all the juicy details about your project.

### How It Works
When you type in something like:

_"Create a serverless project named my_project"_

…here’s what goes on behind the scenes:

- **User Input & Context:** Your natural language command is sent to the AI agent.
- **Function Descriptions:** The AI agent already knows about a few functions—like create_ess_project, delete_ess_project, get_ess_project_status, and get_ess_project_details—because we gave it detailed descriptions. These descriptions tell the AI what each function does and what parameters they need.
- **LLM Processing:** Your query plus the function info is sent off to the LLM. This means the AI sees:
- **The User Query**: Your plain-English instruction.
- **Available Functions & Descriptions**: Details on what each tool does so it can choose the right one.
- **Context/Historic Chat Info**: Since it’s a conversation, it remembers what’s been said before.
- **Function Call & Response**: The AI figures out which function to call, passes along the right parameters (like your project name), and then the function is executed. The response is sent back to you in a friendly format.

In short, we’re sending both your natural language query and a list of detailed tool descriptions to the LLM so it can “understandd” and choose the right action for your request.

### Setup

- **Clone the Repoo:** 
```
git clone git@github.com:framsouza/serverless-ai-agent.git
cd serverless-ai-agent
```

- **Install the Dependencies**: Make sure you have Python installed, then run:
```
pip install -r requirements.txt
```

- **Configure Your Environment**: Create a .env file in the project root with these variables:
```
ES_URL=your_elasticsearch_api_url
API_KEY=your_elasticsearch_api_key
REGION=your_region
OPENAI_API_KEY=your_openai_api_key
```

- **Projects File**: The tool uses a `projects.json` file to store your project mappings (project names to their details). This file is created automatically if it doesn’t exist.

### Running the agent

```
python main.py
```

You’ll see a prompt like this:

```
Welcome to the Serverless Project AI Agent Tool!
You can ask things like:
 - 'Create a serverless project named my_project'
 - 'Delete the serverless project named my_project'
 - 'Get the status of the serverless project named my_project'
 - 'Get the details of the serverless project named my_project'
```

Type in your command, and the AI agent will work its magic! When you're done, type `exit` or `quit` to leave.

### A few more details

- **LLM Integration**: The LLM is given both your query and detailed descriptions of each available function. This helps it understand the context and decide, for example, whether to call `create_ess_project` or `delete_ess_project`.
- **Tool Descriptions**: Each function tool (created using FunctionTool.from_defaults) has a friendly description. This description is included in the prompt sent to the LLM so that it “knows” what actions are available and what each action expects.
- **Persistence**: Your projects and their details are saved in projects.json, so you don’t have to re-enter info every time.
- **Verbose Logging**: The agent is set to verbose mode, which is great for debugging and seeing how your instructions get translated into function calls.



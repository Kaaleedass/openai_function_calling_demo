# OpenAI Function Calling Demo

A practical demonstration of **OpenAI Function Calling / Tool Calling** using Python and the OpenAI Responses API.

This project shows how an OpenAI model can understand a user's request, decide which tool is required, generate the tool arguments, execute the corresponding Python function, and use the tool result to produce a final response.

## 🚀 Features

This demo includes three custom tools:

- 🌤️ **Weather Tool** — Retrieves mock weather information for supported cities.
- 🧮 **Calculator Tool** — Performs addition, subtraction, multiplication, and division.
- 📏 **Unit Conversion Tool** — Converts between meters, feet, inches, kilometers, and miles.

The model automatically selects the appropriate function based on the user's request.

## 🧠 How Function Calling Works

The basic workflow is:

```text
User Request
     ↓
OpenAI Model
     ↓
Select Appropriate Tool
     ↓
Generate Function Arguments
     ↓
Python Executes Function
     ↓
Tool Result Returned to Model
     ↓
OpenAI Model Generates Final Answer
```

For example, a single user request can contain multiple tasks:

> "If I'm travelling 60 miles, how many kilometers is that? And what's 60 divided by 2.5? And what's the weather like in London?"

The model can identify that three different tools are required:

```text
60 miles → kilometers
        ↓
convert_units()

60 ÷ 2.5
        ↓
calculate()

Weather in London
        ↓
get_weather()
```

## 🛠️ Technologies Used

- Python 3.12+
- OpenAI Python SDK
- OpenAI Responses API
- Function Calling / Tool Calling
- JSON
- Python type hints

## 📁 Project Structure

```text
openai-function-calling-demo/
│
├── openai_function_calling_demo.py
├── README.md
├── requirements.txt
└── .gitignore
```

## ⚙️ Installation

### 1. Clone the repository

```bash
git clone https://github.com/YOUR_USERNAME/openai-function-calling-demo.git
cd openai-function-calling-demo
```

### 2. Install the OpenAI SDK

```bash
pip install openai
```

Or:

```bash
pip install -r requirements.txt
```

### 3. Configure your API key

Set your OpenAI API key as an environment variable.

### Windows PowerShell

```powershell
$env:OPENAI_API_KEY="your-api-key"
```

### Windows Command Prompt

```cmd
set OPENAI_API_KEY=your-api-key
```

Do **not** hard-code your API key inside the Python source code.

## ▶️ Run the Example

```bash
python openai_function_calling_demo.py
```

Example input:

```text
If I'm travelling 60 miles, how many kilometers is that?
And what's 60 divided by 2.5?
And, what's the weather like in London?
```

Example output:

```text
60 miles = approximately 96.56 kilometers.

60 divided by 2.5 = 24.

The weather in London is 18°C and cloudy.
```

## 🔧 Available Tools

### 1. `get_weather`

Returns weather information for a given city.

Example:

```python
get_weather(
    location="London",
    unit="celsius"
)
```

Example result:

```json
{
    "location": "London",
    "temperature": 18,
    "unit": "celsius",
    "condition": "Cloudy"
}
```

> The weather data in this project is mock data and is intended only for demonstrating function calling.

### 2. `calculate`

Performs basic arithmetic operations.

Supported operations:

```text
add
subtract
multiply
divide
```

Example:

```python
calculate(
    operation="divide",
    a=60,
    b=2.5
)
```

Result:

```text
24
```

### 3. `convert_units`

Converts between supported distance units.

Supported units:

```text
meters
feet
inches
kilometers
miles
```

Example:

```python
convert_units(
    value=60,
    from_unit="miles",
    to_unit="kilometers"
)
```

Result:

```text
96.5604 kilometers
```

## 🔄 Tool Calling Flow in the Code

The tools are provided to the OpenAI model through the `tools` parameter:

```python
response = client.responses.create(
    model="gpt-4o-mini",
    input=messages,
    tools=functions,
    tool_choice="auto"
)
```

The model can return a function call such as:

```text
function_call
```

The Python application then:

1. Identifies the requested function.
2. Reads the JSON arguments.
3. Executes the corresponding Python function.
4. Sends the result back to the model.
5. Allows the model to generate the final answer.

The tool result is returned using:

```python
{
    "type": "function_call_output",
    "call_id": tool_call.call_id,
    "output": json.dumps(function_response)
}
```

## 🎯 What This Project Demonstrates

This project demonstrates several important concepts used in modern AI applications:

- LLM tool calling
- Structured function arguments
- JSON Schema
- Automatic tool selection
- Multiple tools in a single application
- Tool execution loops
- Returning tool results to an LLM
- Building AI applications with external capabilities

## 🔐 Security

Never commit your OpenAI API key to GitHub.

Use an environment variable:

```text
OPENAI_API_KEY
```

Add sensitive files such as `.env` to `.gitignore`:

```gitignore
.env
__pycache__/
*.pyc
.venv/
venv/
```

## 🚀 Future Improvements

Possible extensions for this project include:

- Replace mock weather data with a real weather API.
- Add web search as a tool.
- Add database query tools.
- Add file/document analysis tools.
- Add email automation tools.
- Add API integrations.
- Add streaming responses.
- Add multi-step agent workflows.
- Add tool error handling and retries.
- Add conversation memory.

## 📚 Learning Objective

The main objective of this project is to understand how an LLM can move beyond simply generating text and instead **select and execute tools based on the user's request**.

This is one of the fundamental building blocks for developing:

- AI Assistants
- AI Agents
- Agentic workflows
- Automation systems
- Tool-using LLM applications

---

## 👨‍💻 Author

**Kaaleedass Manoharan**

Data & AI Automation | Python | Power BI | Tableau | Generative AI | Agentic AI

---

⭐ If you find this project useful, consider giving the repository a star.

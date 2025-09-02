# Data Cleaning Agent

A Jupyter-based agent that leverages LangChain and OpenAI to perform common data-cleaning tasks (e.g., imputing missing values, generating data summaries) via generated Python code.

## Prerequisites

- Anaconda or Miniconda installed
- Git (to clone this repo)
- An OpenAI API key set in your environment (`OPENAI_API_KEY`)

## Setup

### Step 1: Clone the Repository

```bash
git clone https://github.com/Tchanwangsa/Data-Cleaning-Agent_Workshop-Version.git
cd Data-Cleaning-Agent_Workshop-Version
```

### Step 2: Create Conda Environment

**Use Anaconda Prompt (Windows) or Terminal (macOS/Linux):**

```bash
# Create and activate environment
conda create -n data-cleaning-agent python=3.11 -y
conda activate data-cleaning-agent

# Install Jupyter and kernel support
conda install jupyter ipykernel -y
python -m ipykernel install --user --name data-cleaning-agent --display-name "Data Cleaning Agent"
```

**macOS/Linux:** If you get "conda: command not found", run `conda init` and restart your terminal.

### Step 3: Configure API Key

Copy the `.env.example` file or run:

**- Windows:** `copy .env.example .env`  
**- macOS/Linux:** `cp .env.example .env`

Edit the `.env` file and add your OpenAI API key:

```
OPENAI_API_KEY=your_actual_api_key_here
```

### Step 4: Launch Environment

**Jupyter Notebook:**

```bash
jupyter notebook
```

**VS Code:**

```bash
code .
```

**Important:** Select the "Data Cleaning Agent" kernel when opening notebooks. (This is the environment we created in part 2)

### Step 5: Install Dependencies

Open `main.ipynb` and run the first cell:

```python
# Install necessary packages
%pip import-ipynb
...
```

## Adding New Features

1. Create a copy of `features/feature_scaffold.ipynb` and rename to `your_feature.ipynb` and open it in VS Code or Jupyter.
2. In the copied notebook, Replace all the placeholder code and implement your function. Remember to rename `def your_feature(user_query, df):`.
3. Save your notebook and import your feature in `route_qeury.ipynb`, then add it to the features list.

## Additional Useful Tools

- Setup LLM Call tracing with <a href="smith.langchain.com">LangSmith</a>
- Check available models and costs on <a href="https://platform.openai.com/docs/pricing">Open AI</a>

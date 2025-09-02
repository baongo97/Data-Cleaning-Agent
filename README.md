# Data Cleaning Agent

A Jupyter-based agent that leverages LangChain and OpenAI to perform common data-cleaning tasks (e.g., imputing missing values, detecting outliers) via generated Python code.

## Prerequisites

- Anaconda or Miniconda installed
- Git (to clone this repo)
- An OpenAI API key set in your environment (`OPENAI_API_KEY`)

## Setup

1. Clone the repository and enter its folder

   ```bash
   git clone https://github.com/Tchanwangsa/data-cleaning-agent.git
   cd data-cleaning-agent
   ```

2. Create and activate a new conda environment

   ```bash
   conda create -n data-cleaning-agent python=3.xx -y
   conda activate data-cleaning-agent
   ```

3. (Optional) Install Jupyter if it’s not already available (or skip if you prefer VS Code notebooks)

   ```bash
   conda install jupyter -y      # only if using Jupyter
   conda install ipykernel -y    # for VS Code notebook support
   ```

4. Launch Jupyter Notebook (or VSCode)

   ```bash
   jupyter notebook
   ```

5. In the Notebook UI, open `main.ipynb` and run the **first cell** to install all required Python packages:
   ```python
   %pip install import-ipynb pandas numpy sklearn \
               langchain langchain-community openai
   ```

## Adding New Features

1. Copy `scaffold.ipynb` to `features/your_feature.ipynb` and open it in VS Code or Jupyter.
2. In the copied notebook, implement the function `def your_feature(user_query, df):` by replacing the placeholder code.
3. Save your notebook and import your feature in `main.ipynb`, then add it to the features list.

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

## Current Features

The agent currently supports the following data cleaning features:

### 📊 Dataset Summaries (`get_summaries`)
**What it does:** Generates comprehensive statistical summaries for dataset exploration.

**Capabilities:**
- **Numerical summaries:** count, missing values, mean, median, standard deviation, variance, min/max, quartiles, skewness, range, IQR
- **Categorical summaries:** count, missing values, unique values, mode, top frequency
- **Mode statistics:** mode values, mode frequency, unique value counts, most frequent values

**Example queries:**
- "Give me a summary of all numerical columns"
- "Find cardinality of categorical columns" 
- "Show me descriptive statistics for price and age columns"

### 🔧 Missing Values Handler (`missing_vals`)
**What it does:** Intelligently handles missing values using data cleaning best practices.

**Capabilities:**
- **Automatic analysis:** Analyzes missing value patterns and suggests appropriate imputation strategies
- **Smart imputation:** Applies different strategies based on data type and distribution:
  - Numerical: mean (normal distribution) or median (skewed distribution)
  - Categorical: mode for low cardinality, "Unknown" for high cardinality  
  - Datetime: forward/backward fill or interpolation
- **Column dropping:** Automatically drops columns with excessive missing values (>50% by default)

**Example queries:**
- "Handle missing values in my dataset"
- "Suggest ways to impute missing data"
- "Fill missing values with appropriate methods"

### 🔍 Duplicate Detection (`duplicates`)
**What it does:** Intelligently detects and handles duplicate records using exact matching and fuzzy string matching.

**Capabilities:**
- **Exact duplicate detection:** Find rows with identical values across specified columns using pandas `.duplicated()`
- **Near-duplicate detection:** Find similar rows using fuzzy string matching with configurable similarity thresholds
- **Multiple removal strategies:** Remove duplicates keeping 'first', 'last', or 'most_complete' (fewest missing values) records
- **Duplicate flagging:** Add boolean column marking duplicates for inspection before removal
- **Pattern analysis:** Comprehensive analysis showing which columns contribute most to duplicates and duplicate statistics

**Example queries:**
- "Find duplicate rows"
- "Remove duplicate records keeping the first occurrence"
- "Show me similar records in customer data"
- "Analyze duplicate patterns in the dataset"
- "Flag duplicates for review before removal"

### 🔧 Data Type Optimization (`data_types`)
**What it does:** Analyzes and optimizes data types to reduce memory usage and improve performance through intelligent type conversion.

**Capabilities:**
- **Data type analysis:** Comprehensive analysis of current types with optimization suggestions and memory usage breakdown
- **Numeric optimization:** Automatic downcasting of int64→int32/int16/int8 and float64→float32 based on value ranges
- **Date parsing:** Auto-detection and conversion of date strings with multiple format support (YYYY-MM-DD, MM/DD/YYYY, etc.)
- **Percentage conversion:** Convert percentage strings ("50%") to decimal floats (0.5) for mathematical operations
- **Categorical optimization:** Convert low-cardinality string columns to pandas category type for memory savings
- **Boolean detection:** Identify and convert Yes/No, True/False, 1/0, On/Off patterns to boolean type
- **Memory comparison:** Before/after analysis showing exact memory savings and type conversion details

**Example queries:**
- "Optimize data types to save memory"
- "Convert date columns automatically"
- "Fix percentage columns"
- "Analyze current data types"
- "Convert to categorical types"
- "Detect boolean columns"
- "Show memory usage comparison"

### 🎯 Outlier Detection & Handling (`outlier_detection`)
**What it does:** Intelligently detects and handles outlier records using statistical methods (IQR, Z-score) and machine learning approaches (Isolation Forest).

**Capabilities:**
- **IQR method detection:** Find outliers using Interquartile Range method (Q1-1.5*IQR, Q3+1.5*IQR) - robust for skewed data
- **Z-score method detection:** Statistical outlier detection suitable for normally distributed data with configurable threshold
- **Isolation Forest detection:** ML-based multivariate outlier detection that can identify complex patterns across multiple features
- **Multiple handling strategies:** 
  - **Capping:** Limit outliers to boundary values without removing data points
  - **Removal:** Delete outlier rows from the dataset
  - **Log transformation:** Apply logarithmic transformation to reduce outlier impact
- **Comprehensive analysis:** Detailed outlier summary with distribution assessment, skewness analysis, and method recommendations
- **Smart method selection:** Automatic suggestions for best detection method based on data distribution characteristics

**Example queries:**
- "Find outliers in price column"
- "Remove extreme values using IQR method"
- "Show me outlier patterns in the dataset"
- "Cap outliers using Z-score method"
- "Analyze outliers across all numeric columns"
- "Handle outliers with log transformation"

### 📝 Text Processing (`text_processing`)
**What it does:** Comprehensive text cleaning and standardization for improving data quality in text columns.

**Capabilities:**
- **Basic text cleaning:** Remove extra whitespace, standardize encoding, handle special characters
- **Case standardization:** Convert to consistent case formatting (upper, lower, title, sentence case)
- **Special character handling:** Remove or replace special characters with customizable keep-lists
- **Categorical text standardization:** Map text variants to standard values using fuzzy string matching
- **Numeric extraction:** Extract numbers and numeric patterns from mixed text columns
- **Pattern validation:** Validate text against regex patterns for format compliance
- **Text quality assessment:** Comprehensive analysis of text data quality with cleaning recommendations

**Example queries:**
- "Clean text columns"
- "Standardize city names"
- "Extract numbers from product codes"
- "Convert text to title case"
- "Remove special characters from names"
- "Validate email format patterns"

### ✅ Data Validation (`validation`)
**What it does:** Comprehensive data quality validation and compliance checking across multiple data types and formats.

**Capabilities:**
- **Email validation:** Check email format validity using regex patterns and domain validation
- **Phone number validation:** International phone number validation with country code support
- **Numeric range validation:** Validate numeric values against specified min/max boundaries
- **Cross-column consistency checks:** Validate relationships between related columns
- **Categorical value validation:** Check categorical values against allowed master lists
- **Date format validation:** Validate date formats and logical date ranges
- **Comprehensive validation reporting:** Generate detailed validation reports with data quality scores
- **Custom validation rules:** Support for user-defined validation logic

**Example queries:**
- "Validate email addresses"
- "Check if ages are in reasonable range"
- "Find data quality issues"
- "Validate phone number formats"
- "Check categorical values against allowed list"
- "Generate data validation report"

### 🔧 Feature Engineering (`feature_engineering`)
**What it does:** Creates new features from existing data through various transformations to enhance machine learning model performance.

**Capabilities:**
- **Categorical binning:** Create categorical bins from numeric columns using equal-width, equal-frequency, or custom methods
- **Ratio calculations:** Calculate ratios between numeric columns with zero-division handling
- **Feature interactions:** Create interaction features using multiply, add, subtract, divide, mean, max, min operations
- **Time series lag features:** Create lag features (previous values) with support for grouped/panel data
- **Rolling window statistics:** Generate rolling averages, sums, standard deviations, min/max with customizable windows
- **Polynomial transformations:** Create polynomial features using sklearn with configurable degrees
- **Memory usage tracking:** Monitor memory impact of feature engineering operations
- **Smart feature naming:** Automatic generation of descriptive feature names

**Example queries:**
- "Create age groups in 10-year bins"
- "Calculate price per square foot ratio"
- "Generate interaction features between income and education"
- "Add 1 and 2 period lag features for sales"
- "Create 7-day rolling average"
- "Generate quadratic polynomial features"

## Adding New Features

1. Create a copy of `features/feature_scaffold.ipynb` and rename to `your_feature.ipynb` and open it in VS Code or Jupyter.
2. In the copied notebook, Replace all the placeholder code and implement your function. Remember to rename `def your_feature(user_query, df):`.
3. Save your notebook and import your feature in `route_qeury.ipynb`, then add it to the features list.

## Additional Useful Tools

- Setup LLM Call tracing with <a href="smith.langchain.com">LangSmith</a>
- Check available models and costs on <a href="https://platform.openai.com/docs/pricing">Open AI</a>

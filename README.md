## About This Fork

This repository extends [Microsoft lida](https://github.com/microsoft/lida) to natively support automated data summarization, visualization using local Ollama language models. With this enhancement, LIDA users are no longer restricted to cloud-based LLM providers—charts, summaries, and infographics can now be generated locally on your own machine using any LLM supported by Ollama.

Based on testing, llama3.1:8b produces the most reliable output for JSON-format generation. Other models showed inconsistencies in producing valid JSON, causing processing failures.


### Additional Supported LLM Providers

- **Ollama models** (added through the [`llmx-ollama-extension`](https://github.com/sunishbharat/llmx-ollama-extension) integration)

> **Note:** Ollama support is enabled via the `llmx-ollama-extension` repository. Make sure to install this extension for local model compatibility.

## Setup

Clone [llmx-ollama-extension](https://github.com/sunishbharat/llmx-ollama-extension) and install it:

```
git clone <this_repo>
cd <this_repo>
```

### Remove existing LLMX (if installed) in environment
--------------------------------------------------
```
pip uninstall llmx
```

### Setup conda env
---------------
```
conda create --name <new_env> python=3.12.11
conda activate <new_env>
```

### Clone `llmx-ollama-extension` repo locally
-------------------------------------
It would be recommended to clone it outside the LIDA repo folder:
```
git clone https://github.com/sunishbharat/llmx-ollama-extension.git
cd llmx-ollama-extension
```


From within your llmx-ollama-extension folder:
```
pip install -e .
```

### Install lida and all necessary dependencies
----------------------------------------
Return to your lida repo folder:
```
cd ../lida
pip install -e .
pip install -r requirements.txt
```
Install any extras or dev dependencies if needed:
```
pip install lida[dev]
```


### Sample Output using OLLAMA_LLM_MODEL = "llama3.1:8b"

```
python lida\tests\test_components.py
```
```text
summary_enrich["dataset_description"]='This dataset contains information about various car models including their names, types, prices,
engine sizes, horsepower, city and highway miles per gallon, weight, wheel base, length, and width. The data is based on real-world
cars available in the US market.'

goal=Goal(question="What type of car has the highest average 'Retail_Price'?", visualization='bar chart of Type vs Average(Retail_Price)
using [Type, Retail_Price] from dataset', rationale='This will help identify which car types are associated with higher prices.
We can use bar charts instead of pie charts because they are more informative and easy to read. This visualization is relevant for a
data analyst who wants to understand the relationship between Type and Retail Price.', index=0)

goal=Goal(question="What region has the highest number of 'City_Miles_Per_Gallon' over 60?", visualization='choropleth map of
City_Miles_Per_Gallon > 60 using [Name, City_Miles_Per_Gallon] from dataset', rationale="This will help us understand where cars
 with good fuel efficiency are located. We can use a choropleth map because it's easy to interpret and allows for spatial analysis.
This visualization is relevant for a data analyst who wants to identify areas with good fuel efficiency.", index=1)

goal=Goal(question='Which type of cars have higher horsepower and better fuel efficiency?', visualization='bar chart comparing average
Horsepower_HP_ by Type', rationale='This visualization will help us understand which types of cars (e.g. SUV, Minivan, Sports Car) tend
to have higher horsepower and better fuel efficiency, allowing the data analyst to identify trends in car design and performance.', index=0)


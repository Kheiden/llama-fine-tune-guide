# survival-model-1b

A 1.2B parameter model which has been fine tuned to provide succinct, wilderness survival advice.

WARNING: This is an experiment. Do not rely solely on this model in life threatening situations.


This model is a finetuned version of `meta-llama/Llama-3.2-1B-Instruct`.



## Fine tuning

Prerequisite: Ensure that UV is installed on your system.

Setup the dependencies
```
uv init
uv add -r requirements.txt
```

Optional: Update the dataset at `data/survival.csv`

Run the training:
```
uv run --env-file .env python .\train_fine_tune.py
```

Note: Using a ~5 GHz processor with 128GB of DDR5, I was able to complete the fine tuning in about 30 minutes. 

After training, test the model output:
```
uv run --env-file .env python .\test_fine_tune.py
```

## Using with Ollama

On the host machine, copy the model to the container
```
cd fine-tuned-model
docker cp . ollama:/root/survival-model-1b
```

Within the docker container, create the ollama model
```
bash -
cd /root/survival-model-1b
ollama create survival-model-1b
```

More info:
https://github.com/ollama/ollama/blob/main/docs/import.md#Importing-a-model-from-Safetensors-weights


## Dataset Generation

Gemini 2.0 Flash was used to generate question / answer pairs using the following prompt sequence:

```
"Come up with a list of 100 questions that could be asked by an individual in a survival situation. do NOT repeat questions.
Output the questions using newline delimiters and do NOT number the questions. Do not prefix the questions with any characters, instead add each question on each line"

[GEMINI OUTPUTS TEXT]

"Excellent. Now for each question in this list, provide an answer. Make sure to provide the answer directly following the question in CSV format "question","answer". Make sure to use double quotation marks over both the questions and the answers. Do not forget the comma. Add a newline character after each answer."
```
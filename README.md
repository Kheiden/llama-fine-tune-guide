# llama-fine-tune-guide
If you want to harness the power of the newly released Llama-3.2 lightweight models you're in the right place.

From this [blogpost](https://medium.com/@alexandros_chariton/how-to-fine-tune-llama-3-2-instruct-on-your-own-data-a-detailed-guide-e5f522f397d7)

1. **Add Your Dataset**: Place your CSV file in the `data/` directory of the project. For example, name it `my_dataset.csv`.

2. **Update the Training Script**: Modify the training script to point to your dataset instead of `data/sarcasm.csv`.

3. **Run**: ```python train_fine_tune.py```

4. **Test**: Test the model that was just fine-tuned by running ```python test_fine_tune.py```

For my case, using `data/sarcasm.csv`, I generated this [masterpiece](https://huggingface.co/AlexandrosChariton/SarcasMLL-1B)

---


```
uv init
uv add -r requirements.txt
```

```
uv run --env-file .env python .\train_fine_tune.py
```

```
uv run --env-file .env python .\test_fine_tune.py
```

## Using with Ollama

On the host machine
```
cd fine-tuned-model
docker cp . ollama:/root/survival-model-1b
```

Within the docker container
```
bash -
cd /root/survival-model-1b
ollama create survival-model-1b
```


More info:
https://github.com/ollama/ollama/blob/main/docs/import.md#Importing-a-model-from-Safetensors-weights


# Portfolio Piece: Word Embeddings → Attention 

## What this project is
This is a small NLP portfolio notebook that shows my understanding two important ideas:

1) **Word embeddings** (Word2Vec / GloVe / fastText style vectors)  
2) **Scaled dot-product attention** (the math behind Transformers)

Then I connect them: I take word vectors for a sentence and run **self-attention** to see “who attends to who”.

I’m not training a big model here. The point is: clean implementation + clear inspection.

## Files
- `notebooks/main_analysis_FINAL.ipynb` → the full walkthrough
- `outputs/` → saved figures + small tables created by the notebook
- `requirements.txt` → packages used

## What outputs you should see 
When you run the notebook, it prints + plots a few things:

### 1) Nearest neighbors
You’ll see lists like “Neighbors for 'king' …” with similarity scores.
This shows which words are close in the embedding space.

### 2) Analogies
You’ll see examples like:
`man : king :: woman : ?`
This is the classic vector arithmetic idea: **v(king) - v(man) + v(woman)**.

### 3) Bias-style probe table
You’ll see a small table (`bias_df`) with columns like:
- `sim_to_male`
- `sim_to_female`
- `male_minus_female`

This is a simple way to show that embeddings can have different association patterns.
It is **not** a full bias audit, just a small demo.

### 4) PCA plot of word clusters
A 2D scatter plot that groups related words.
This is just for intuition (PCA changes the shape, but you can still see clusters).

### 5) Attention heatmaps
Heatmaps show attention weights (rows are queries, columns are keys).
You’ll see:
- random attention (sanity check)
- multi-head attention (head 0)
- self-attention over a sentence (head 0)

### 6) “it” attention printout
For a few heads, it prints the top tokens that “it” attends to.
This is not true coreference resolution, but it shows how to inspect attention.

## Where outputs are saved
The notebook saves files into `outputs/` automatically:
- `pca_words.png`
- `attention_random_qkv.png`
- `mha_head0.png`
- `self_attention_sentence_head0.png`
- `bias_probe_table.csv`
- `attn_random_qkv.npy`
- `attn_mha_sanity.npy`
- `attn_sentence.npy`

## How to run
### Recommended (Python 3.12)
Matplotlib can be shaky on Python 3.13 right now, so I recommend Python 3.12.

1) Create a virtual environment
```bash
python3.12 -m venv .venv
source .venv/bin/activate
```

2) Install dependencies
```bash
pip install -U pip
pip install -r requirements.txt
```

3) Run the notebook
```bash
jupyter lab
```
Open `notebooks/main_analysis_FINAL.ipynb`.

## Notes / limitations (short)
- Embeddings here are **static** (one vector per word, no context).
- The bias probe is small and not a full evaluation.
- Attention is not trained on a task in this notebook — it’s showing the mechanism.

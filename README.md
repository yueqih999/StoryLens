# Narrator
## Project Structure
```
Narrator/
├── data/                       # Raw text data
├── embeddings/                 # Stored embeddings
│   ├── all_embeddings.pkl      # Main embedding file
│   ├── embedded_chapter.csv    # Processed text for each chapter
│   ├── similarity_chapter.json # Cosine similarity for each chapter
│   └── similarity_matrix.npy   # Similarity matrix for each chapter
├── output/                     # Output visualizations and analysis
│   ├── umap_results/           # UMAP visualizations
│   ├── hierarchy/              # Hierarchical clustering results
│   └── graph/                  # Graph analysis results
├── 0model/                     # Model training, text preprocessing and embedding scripts, finished
├── 1visualization/             # Visualization scripts, finished
├── 2hierarchy/                 # Hierarchical analysis, in progress
└── 3rag/                       # Retrieval based accurate matching and semantic search, finished
```

## Current Progress
- **Model Initial & Training**: Completed
- **Text Preprocessing & Embedding**: Completed
- **Visualization & Clustering**: Completed
- **Hierarchical Analysis**: Completed
- **Retrieval-Augmented Generation**: Completed

## Guide
```bash
pip install -r requirements.txt
``` 

## 0 model
The training code is under a CPU environment and we use Bookcorpus dataset(0.5%) to train the pretrain-model 'all-MiniLM-L6-v2': https://huggingface.co/datasets/bookcorpus/bookcorpus
```bash
python 0model/model.py
``` 
The trained model will be saved at model/.
Then upload your txt file in data/, run:
```bash
python 0model/text_process.py
python 0model/embedding.py
``` 
You will get similarity matrix, MI(mutual information), and embedded sentences.
![model training methods](display/training_progress.png)

## 1 visualization
Based on calculated sentence embeddings, we use UMAP to do clustering and visualization: https://umap-learn.readthedocs.io/en/latest/basic_usage.html 
```bash
python 1cluster/cluster_umap_viz.py
``` 
![clustered points result](display/points.png)
![connectivity result](display/connectivity.png)
![bundling result](display/bundling.png)

## 2 hierarchy
We provide two visualization options, both based on MI values:
```bash
python 2hierarchy/hierarchy_viz.py  # radial 
python 2hierarchy/hierarchy.py  # tree
``` 
![radial hierarchy analysis result](display/word_hierarchy_radial.png)

## 3 rag
The codes firstly do an accurate retrival, if there is no matching results, it will return top-5 results based on semantic search.
```bash
python 3rag/retrival_word.py
``` 

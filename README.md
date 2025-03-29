# 🎭 To Train or Not to Train: That is the Question

## 🔥 Overview
This project implements a character-level GPT model trained on Shakespeare's writings. The model follows the architecture described in the \"Attention is All You Need\" paper, with modifications suited for character-level language modeling. This repository explores data preprocessing, model architecture, training methodology, and performance metrics.

## 📖 Project Description
This is a decoder-only transformer, GPT-style model, designed to predict the next character in a sequence using Shakespeare's texts. Character-level models have unique advantages over word-level models, such as handling out-of-vocabulary words and learning morphological patterns.

---
## 🛠️ Data Preprocessing

### 1.1 Dataset Loading and Character Tokenization
- Loaded the Shakespeare dataset and tokenized it at the character level.
- Created a vocabulary of all unique characters in the text.
- Assigned each character a unique integer index.

### 1.2 Sequence Generation
- Each input sequence is paired with a corresponding target sequence, shifted by one character.
- This enables the model to learn next-character prediction based on the current sequence.

---
## 🏗️ Model Architecture

### 2.1 Transformer Block
- Implements self-attention and a feed-forward network.
- Layer normalization is applied before multi-head attention and feed-forward networks to improve training stability.
- Uses **GELU** activations instead of ReLU for better performance.

### 2.2 Positional Encoding
- Transformers lack inherent sequence order knowledge.
- Sinusoidal positional encodings provide relative positional information for the characters.

### 2.3 GPT Model
The full GPT model integrates embeddings, positional encodings, and multiple transformer blocks. The architecture consists of:
- **Embedding dimension**: 192
- **Number of attention heads**: 6
- **Feed-forward dimension**: 768
- **Number of transformer layers**: 6
- **Sequence length**: 125

### 2.4 Causal Masking
- Ensures the model does not \"look ahead\" at future tokens.
- Uses an upper triangular mask to maintain the autoregressive property.

---
## 🎯 Training Methodology

### 3.1 Optimizer and Learning Rate
- **Optimizer**: AdamW
- **Learning Rate Schedule**: Linear warmup followed by cosine decay.
- Helps stabilize training and improves convergence.

### 3.2 Training Loop
The training loop includes:
- **Loss function**: Cross-entropy loss for next-character prediction.
- **Gradient clipping**: Prevents exploding gradients.
- **Early stopping**: Based on validation loss.
- **Model checkpointing**: Saves the best-performing model.
- **Timing information**: Tracks training progress.
- **Text generation at intervals**: Evaluates qualitative improvements.
- **Sampling techniques**: Uses temperature and nucleus sampling for natural text generation.

### 3.3 Hyperparameters
- **Batch size**: 64
- **Initial learning rate**: 0.0003
- **Warmup steps**: 1000
- **Dropout rate**: 0.2
- **Maximum epochs**: 40 (with early stopping)
- **Patience for early stopping**: 25 epochs

---
## 📊 Results

### 4.1 Training Process
- The model was trained for **40 epochs**.
- Sample outputs were generated every **5 epochs**.

### 4.2 Performance
- The model successfully learns to generate Shakespearean-style text.
- Improved loss and perplexity over epochs.
- Demonstrates effective character-level language modeling.



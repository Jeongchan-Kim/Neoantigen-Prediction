# NeoAntigen prediction

The Neoantigen prediction model is a computational approach that uses machine learning algorithms to predict the likelihood that a peptide sequence derived from a tumor-specific mutation can bind to major histocompatibility complex (MHC) molecules and elicit an immune response. Neoantigens are antigens that arise from somatic mutations in cancer cells, and they are potentially useful targets for cancer immunotherapy.

The prediction model takes as input the amino acid sequence of the mutant peptide and the patient's MHC type. It then calculates a score indicating the likelihood that the peptide will bind to the MHC molecule and be presented to T cells, which can then recognize and target the cancer cells.

The accuracy of neoantigen prediction models is critical to the success of cancer immunotherapy, as the selection of immunogenic neoantigens is a key factor in determining the efficacy of the treatment. Machine learning algorithms are particularly useful for this task because they can learn from large datasets of known neoantigens and MHC-peptide binding affinities to predict the likelihood of new peptides being immunogenic.

Overall, neoantigen prediction models have the potential to greatly improve the selection of personalized cancer immunotherapies by identifying the most promising neoantigens for each patient.
## Data Preprocessing

1. Load the raw data from a CSV file using Pandas, where each row represents a peptide sequence and its corresponding binding affinity to a particular MHC class I molecule.

2. Convert the amino acid sequences into numerical feature vectors using a one-hot encoding scheme. Each amino acid is represented by a vector of length 20, with a 1 in the position corresponding to the amino acid and 0s elsewhere. The resulting feature matrix has dimensions (n_samples, sequence_length, 20).

3. Generate a binary matrix indicating the presence or absence of each amino acid at each position in the sequence. This matrix has dimensions (n_samples, sequence_length, 1).

4. Merge the one-hot encoded feature matrix and the binary matrix into a single feature matrix, which has dimensions (n_samples, sequence_length, 21). This matrix is used as the input to the model.

5. Split the data into training and validation sets using a 80/20 split.
## About the Model

### Feature extractor
The feature extractor is based on a multi-layered encoder architecture, which is designed to learn a distributed representation of the peptide sequences. The encoder is composed of multiple layers of self-attention blocks followed by feedforward layers. The self-attention blocks are responsible for attending to different parts of the peptide sequence and extracting meaningful features, while the feedforward layers transform the features into a lower-dimensional representation.

### Encoder architecture
The encoder architecture used in the NeoAntigen prediction model combines self-attention blocks and feedforward layers to create a powerful and flexible feature extractor. Each layer of the encoder consists of a multi-head self-attention mechanism, which allows the model to attend to different parts of the peptide sequence simultaneously, and a feedforward neural network that applies a non-linear transformation to the attended features. The output of each layer is then passed through a layer normalization operation and a residual connection before being fed into the next layer. The final output of the encoder is a fixed-length vector representation of the input peptide sequence, which is used as input to the prediction model.

### Prediction model
The prediction model takes the output of the encoder as input and uses a series of fully connected layers to predict the binding affinity of the peptide sequence to MHC class I molecules. The prediction model uses a binary cross-entropy loss function to optimize the model's parameters during training, and the accuracy of the model is evaluated using the area under the receiver operating characteristic curve (AUC-ROC) on a held-out test set.
## Result

Validation at Epoch 20, AUROC: 0.94872 , AUPRC: 0.88222 , F1: 0.79661 , Cross-entropy Loss: 3.72805

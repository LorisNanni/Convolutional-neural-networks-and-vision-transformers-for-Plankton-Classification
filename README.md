# Convolutional-neural-networks-and-vision-transformers-for-Plankton-Classification

ToolPlankton2024_matlab.rar code for training ensemble of CNNs, matlab code, see the README inside that .rar for details on how to run and modify the functions.

transformer_ens.zip is the code for training transformers, pytorch code

In our example code, we use WHOI dataset stored in a .mat file, you can download it from: https://zenodo.org/records/12797119

for combining scores of CNNs and transformers ensemble, remember to normalize the scores (separately) by the number of classifiers that belong to each ensemble, before the weighted sum rule, therefore: 
a) sum rule among the CNNs, divide that score by the number of CNNs that belong to the ensemble of CNNs;
b) sum rule among the transformers, divide that score by the number of transformers that belong to the ensemble of transformers;
c) weighted sum rule considering the normalized score obtained in the previous step a) and b).

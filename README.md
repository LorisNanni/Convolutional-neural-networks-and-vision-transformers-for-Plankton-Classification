# Convolutional-neural-networks-and-vision-transformers-for-Plankton-Classification

ToolPlankton2024_matlab.rar code for training ensemble of CNNs, matlab code, see the README inside that .rar for details on how to run and modify the functions.

transformer_ens.zip is the code for training transformers, pytorch code

In our example code, we use WHOI dataset stored in a .mat file, you can download it from: https://zenodo.org/records/12797119

Notice that (as detailed in the paper): "For CNNs in the CrossD dataset, we adjusted the pixel values of all
patterns in the training and test sets to match the average pixel values of the training set. Additionally, we incorporate an extra control mechanism
during training. At each epoch, we record the corresponding loss and, for inference, select the network from the epoch with the lowest recorded loss.
This approach is necessary due to the instability of convergence. Without this processing, performance would significantly deteriorate"
you have to add in the code the following lines after reading an image (i.e. the line: IM=NX{DIV(fold,pattern)};), clearly for both training and test sets:

media=mean(IM(:));

sposto=AVG_TR-media;%AVG_TR is the average value of the training images, you have to pre-calculate it

IM=IM+sposto;


for selecting  the network from the epoch with the lowest recorded loss, you can modify in the following way:


rec=inf;

for epoch = 1:numEpochs

...

   for i = 1:numIterationsPerEpoch
   
       ...
       
        valoreLoss(i)=loss;
        
   end
   
   if mean(valoreLoss)<rec
   
      rec=mean(valoreLoss)
      
      dLfin=dlnet;
      
   end

end

%the you use dLfin for classifyng test data
   
for combining scores of CNNs and transformers ensemble, remember to normalize the scores (separately) by the number of classifiers that belong to each ensemble, before the weighted sum rule, therefore: 
a) sum rule among the CNNs, divide that score by the number of CNNs that belong to the ensemble of CNNs;
b) sum rule among the transformers, divide that score by the number of transformers that belong to the ensemble of transformers;
c) weighted sum rule considering the normalized score obtained in the previous step a) and b).

# **FSDL Project Notes**

This documents the FSDL Land Segementation projects progress

[toc]

## Experiment Tracking and Training

Forked the LandCoverSegementation github repo. 

Successfully ran the train.py code.

- There was half precision error THis was solved when the all the weights and images were converted to full precision (https://towardsdatascience.com/understanding-mixed-precision-training-4b246679c7c4)

- Wrote preliminary code to experiment tracking

  - Metrics to track
    - Loss
      - training loss, validation loss
      
    - Performance Metrics
    
      https://towardsdatascience.com/metrics-to-evaluate-your-semantic-segmentation-model-6bcb99639aa2
    
      - IoU, mIoU, DiceLoss
  
  Visualization 
  
  https://www.kaggle.com/code/balraj98/deepglobe-land-cover-classification-deeplabv3
  
- Preprocessing

  - 

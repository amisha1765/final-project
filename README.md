# Architecture Style Detector

This project detects the style of architecture from an image and outputs what type it is. The types is identifies between 12 classes, that are: American craftsman style, Art Nouveau architecture, Baroque architecture, Colonial architecture, Deconstructivism, Georgian architecture, Gothic architecture, Greek Revival architecture, Palladian architecture, Postmodern architecture, Romanesque architecture, and Russian Revival architecture. Keep in mind that becuase architecture styles are a little difficult to differenciate between, and I did not have enough time to train resnet-18 to a sufficient level, the detection is not completely accurate. 

The orginal dataset that I used is from Kaggle, and I worked to alter the dataset as it contained even more classes. The dataset comtains arounf 70% of the images in train, 15% in Validation, and 15% in Test. 

The program was trained using the existing file, train.py, in the jetson-inference directory. After training, I exported the model into an ONXY format.

## The Algorithm

This poject is made from re-training resnet-18 and it uses image-net to identify some of the different types of architecture styles. The pictures from the test dataset can be tested in two different ways, one way is to achive the output on  a .jpg with the detection confidence on top of the image, or the classification python file can be used to just recieve a printed message in the terminal. If you want to traint the program on your own, keep in mind that it takes a very long time and you have to go through a lot of epochs.  

## Running this project

1. Make sure you have resnet-18 already downloaded onto your jetson.
2. All of the files in the github should be downloaded onto the jetson.
3. Change directories into jetson-inference/python/training/classification/data
4. Download the data from the "architecture-dataset" folder, and download that onto the jetson by getting the download link and typing "get" and then the link.
5. unzip the file, by running "unzip", and then the link we just did wget to.
6. Go to back the jetson-inference folder and run: ./docker/run.sh
7. Then again go back into jetson-inference/python/training/classification while in docker.
8. To train the data, run the following: python3 train.py--model-dir=models/architecture-dataset data/architecture-dataset
9. Allow the resnet-18 model to train (as this dataset is complex, try to train it for atlest 20 epochs), but the more training that is done, the better.
10. Make sure to leave docker after training.
11. Then, make sure the onnx_export.py file is on the jetson.
12. Stay in the jetson-inference/python/training/classification folder.
13. Run: python3 onnx_export.py --model-dir=models/architecture-dataset.
There should be a model named resnet18.onnx in jetson-inference/python/training/classification/models/architecture-dataset.

Outputs
1. To see the overall accuracy of the trained model, go to the jetson-inference/python/training/classification, and type: python3 train.py -e --model-dir=models/final_project data/architecture-dataset.
2. In order to get a visual representation of the data, in your home terminal, type: imagenet.py --model=$NET/resnet18.onnx --input_blob=input_0 --output_blob=output_0 --labels=$DATASET/labels.txt $DATASET/test/image.jpg name.jpg
3. You can also use the classification.py file to see the output in terminal. 

[View a video explanation here](video link)

## Conclusion
I belive that this project, when perfected, can help architecture students and people who have an interest in architecture learn and test themselves about some of the different styles of architecture. 
While this project requires more training and is by no means perfect, if I had more time to work on this project, I would work on making this more user friendly and train the model more. 
I hope you enjoyed my project!

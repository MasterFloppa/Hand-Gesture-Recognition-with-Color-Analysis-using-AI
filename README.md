# Hand Gesture Recognition with Color Analysis using AI

## Methodology
This paper introduces an AI-based hand gesture recognition system integrating unique color identification techniques, enhancing precision in human-computer interaction. The approach combines traditional gesture recognition algorithms with color detection techniques. This innovation has broad adaptability across virtual reality, gaming, healthcare, and smart environments, allowing users to convey commands and gain control through color-enhanced gestures. In healthcare, the system can offer a non-intrusive means for professionals to interact with digital interfaces, reducing contamination risks. The paper details the system's design, implementation, and evaluation, showcasing enhanced accuracy and user satisfaction, contributing valuable insights to the evolving field of AI-based gesture recognition and digital interaction. The code will be available at https://github.com/MasterFloppa/Hand-Gesture-Recognition-with-Color-Analysis-using-AI
<br> 
## Data Collection
A diverse and comprehensive data set of hand gestures, encompassing various shapes and movements, has been meticulously collected for both training and testing the AI model. The data is structured in a (x, y) coordinate system, where the positional information is utilized during the model training process.
The incorporation of the media-pipe system proves instrumental in optimizing the model's efficiency. By cropping the image to focus specifically on the hand, the system abstracts the environment, reducing noise and enhancing the model's ability to discern gestures accurately. Notably, the 0th point serves as a reference, establishing the origin for all other points in the coordinate system.
In parallel, the color data set within the model encompasses the pixel color scheme at these defined coordinates. This information facilitates the model's ability to recognize not only the spatial characteristics of hand gestures but also the associated color cues. This comprehensive approach to data set creation and utilization ensures a robust and versatile training foundation for the AI model, contributing to its efficacy in hand gesture recognition with integrated color identification.
The dataset is generated dynamically. The key 'k' starts the dataset creation process. Once pressed, the program takes continuous snippets of the hand gesture displayed on the screen on the press of a key. This data is then retrained and used by the system.

This repository contains the following contents.
* Sample program
* Hand sign recognition model(TFLite)
* Finger gesture recognition model(TFLite)
* Learning data for hand sign recognition and notebook for learning
* Learning data for finger gesture recognition and notebook for learning

# Requirements
* mediapipe 0.8.1
* OpenCV 3.4.2 or Later
* Tensorflow 2.3.0 or Later<br>tf-nightly 2.5.0.dev or later (Only when creating a TFLite for an LSTM model)
* scikit-learn 0.23.2 or Later (Only if you want to display the confusion matrix) 
* matplotlib 3.3.2 or Later (Only if you want to display the confusion matrix)

# Demo
Here's how to run the demo using your webcam.
```bash
python app.py
```

The following options can be specified when running the demo.
* --device<br>Specifying the camera device number (Default：0)
* --width<br>Width at the time of camera capture (Default：960)
* --height<br>Height at the time of camera capture (Default：540)
* --use_static_image_mode<br>Whether to use static_image_mode option for MediaPipe inference (Default：Unspecified)
* --min_detection_confidence<br>
Detection confidence threshold (Default：0.5)
* --min_tracking_confidence<br>
Tracking confidence threshold (Default：0.5)

### app.py
This is a sample program for inference.<br>
In addition, learning data (key points) for hand sign recognition,<br>
You can also collect training data (index finger coordinate history) for finger gesture recognition.

### keypoint_classification.ipynb
This is a model training script for hand sign recognition.

### model/keypoint_classifier
This directory stores files related to hand sign recognition.<br>
The following files are stored.
* Training data(keypoint.csv)
* Trained model(keypoint_classifier.tflite)
* Label data(keypoint_classifier_label.csv)
* Inference module(keypoint_classifier.py)

### model/keypoint_classifier_color
This directory stores files related to color recognition.<br>
The following files are stored.
* Training data(color.csv)
* Trained model(color.tflite)
* Label data(keypoint_classifier_color_label.csv)
* Inference module(keypoint_classifier_color.py)

### utils/cvfpscalc.py
This is a module for FPS measurement.

# Training
Hand sign recognition and finger gesture recognition can add and change training data and retrain the model.

### Hand sign recognition training
#### 1.Learning data collection
Press "k" to enter the mode to save key points（displayed as 「MODE:Logging Key Point」）<br>
<img src="https://user-images.githubusercontent.com/93679609/284384195-72ae5585-9633-4f3a-9670-a002c870e59a.PNG" width="60%"><br><br>
If you press "0" to "9", the key points will be added to "model/keypoint_classifier/keypoint.csv" as shown below.<br>
1st column: Pressed number (used as class ID), 2nd and subsequent columns: Key point coordinates<br>
<img src="https://user-images.githubusercontent.com/37477845/102345725-28d26280-3fe1-11eb-9eeb-8c938e3f625b.png" width="80%"><br><br>
The key point coordinates are the ones that have undergone the following preprocessing up to ④.<br>
<img src="https://user-images.githubusercontent.com/37477845/102242918-ed328c80-3f3d-11eb-907c-61ba05678d54.png" width="80%">
<img src="https://user-images.githubusercontent.com/37477845/102244114-418a3c00-3f3f-11eb-8eef-f658e5aa2d0d.png" width="80%"><br><br>
In the initial state, three types of learning data are included: open hand (class ID: 0), close hand (class ID: 1), and pointing (class ID: 2).<br>
If necessary, add 3 or later, or delete the existing data of csv to prepare the training data.<br>
<img src="https://user-images.githubusercontent.com/93679609/284384516-acce9b4d-8946-41b1-89ad-85599d1100d1.PNG" width="25%">

#### 2.Model training
Open "[keypoint_classification.ipynb](keypoint_classification.ipynb)" in Jupyter Notebook and execute from top to bottom.<br>
To change the number of training data classes, change the value of "NUM_CLASSES = 3" <br>and modify the label of "model/keypoint_classifier/keypoint_classifier_label.csv" as appropriate.<br><br>

#### X.Model structure
The image of the model prepared in "[keypoint_classification.ipynb](keypoint_classification.ipynb)" is as follows.
<img src="https://user-images.githubusercontent.com/37477845/102246723-69c76a00-3f42-11eb-8a4b-7c6b032b7e71.png" width="50%"><br><br>

# Reference
* [MediaPipe](https://mediapipe.dev/)
 
# License 
hand-gesture-recognition-using-mediapipe is under [Apache v2 license](LICENSE).

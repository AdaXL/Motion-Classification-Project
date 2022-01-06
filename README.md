# Motion-Classification-Project

The project's code and report are in https://drive.google.com/drive/folders/1oEj1OSbe0rvz2S4miXhFfETGq1h8zyow?usp=sharing

Please leave a message when requesting access to the link.

## Descriptions:

Data source: https://www.csc.kth.se/cvap/actions/

Link-1 has ALL input videos(input folder) and output video/images(output folder): <s>https://drive.google.com/drive/folders/1wR_utk4PSs_z8g6mQsiJ3_-Zap11Pyhv?usp=sharing</s> (archieved)

Link-2 has the DEMO output video: <s>https://drive.google.com/file/d/1XxY98AE1I6-tHJv22PMWPaAIyihoA6D_/view?usp=sharing</s> (archieved)

Files:

- run.py: single entry point to run the whole project
- utils.py: utility functions, mostly copied from previous homework
- MHILearner.py: a customized knn learner object
- MHIHelper.py: helper functions for building MHI steps(i.e. calculate MHI, Hu Moment, etc.)
- MHIModel.py: model frame, learning from input video and save test output
- 00sequences.txt: a frame reference file downloaded from data source
- requirements.yaml: use this file to build the environment to run the project
- input/: store all input training and testing videos
- output/: store all output video and images

Hierarchy should look like: 

- MHI/(all the .py .yaml .md files listed above)
- MHI/input/(all your downloaded files from Link-1's input folder)
- MHI/output/(all your output files after running the project)

## Instructions:

*Note: This instruction is for Mac users since I used Mac to develop this project. Please adjust accordingly if you are using other devices.*

1. Download and unzip the `MHI.zip` file:
```bash
cd MHI
ls -F
```
If `input/` and `output/` do not exist, please create these folders under `MHI/` by doing:
```bash
mkdir input
mkdir output
```

2. Install environment described in requirements.yaml:

Especially note that I'm using `matplotlib=3.1.2` instead of `matplotlib=3.1.1` which is our previous homework setup, because `matplotlib=3.1.2` fixed a plotting bug.
```bash
conda env create -f requirements.yaml
```

3. Activate environment:
```bash
conda activate Final_Proj
```

4. Download all files from `input/` folder into your local `input/` folder. Note that the file hierarchy should look as indicated the above.


5. Run the project:
```bash
python run.py
```

You should get results like this in your terminal:
```bash
(Final_Proj) risous-MacBook-Pro:MHI lixiang$ python run.py
==================================================
Training...
action:  boxing
action:  handclapping
action:  handwaving
action:  jogging
action:  running
action:  walking
Plotting Confusion Matrix and Printing Accuracy...
Accuracy for validation:  0.875
label  :  [0, 0, 0, 0, 1, 1, 1, 1, 2, 2, 2, 2, 3, 3, 3, 3, 4, 4, 4, 4, 5, 5, 5, 5]
predict:  [0, 1, 1, 0, 1, 1, 1, 1, 2, 2, 2, 4, 3, 3, 3, 3, 4, 4, 4, 4, 5, 5, 5, 5]
==================================================
Testing...(video with ALL actions)
action:  boxing
action:  handclapping
action:  handwaving
action:  jogging
action:  running
action:  walking
Saving Testing Video...(ALL actions)
Plotting Confusion Matrix and Printing Accuracy...
Accuracy for testing:  0.9166666666666666
label  :  [0, 0, 0, 0, 1, 1, 1, 1, 2, 2, 2, 2, 3, 3, 3, 3, 4, 4, 4, 4, 5, 5, 5, 5]
predict:  [0, 0, 0, 0, 1, 1, 1, 1, 2, 2, 2, 2, 3, 3, 4, 3, 2, 4, 4, 4, 5, 5, 5, 5]
==================================================
Testing...(video with SINGLE action)
some randomly chosen samples for different actions:
label: boxing	 predict: boxing	 correct
label: handclapping	 predict: handclapping	 correct
label: handwaving	 predict: handwaving	 correct
label: jogging	 predict: walking	 incorrect
label: running	 predict: running	 correct
label: walking	 predict: walking	 correct
```

6. How to add more test video:

- For video that includes multiple actions:

Note that the output testing video I generated is testing for all actions. If you want to test out an arbitrary video with multiple actions, you'll need to modify file `MHIModel.py`.

You'll need to change the start and end frame in `self.frame_test` accordingly to match with the patterns in `self.sequences`. And you'll need to add or remove actions based on your chosen video.

Then, calling `predict_and_save_video()` will predict and generate the output video.

- For video that has only one action:

Call `predict_single_and_print_label()` to get the predicted label. If you want an output video for this as well, you can simple use the first multiple actions video option, and follow the instructions in that part.


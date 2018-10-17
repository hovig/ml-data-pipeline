DATA 622 # hw2

	Assigned on September 27, 2018
	Due on October 17, 2018 11:59 PM EST
	15 points possible, worth 15% of your final grade

1. Required Reading

	Read Chapter 5 of the Deep Learning Book
	Read Chapter 1 of the Agile Data Science 2.0 textbook

2. Data Pipeline using Python (13 points total)

	Build a data pipeline in Python that downloads data using the urls given below, trains a random forest model on the training dataset using sklearn and scores the model on the test dataset.

	Scoring Rubric

	The homework will be scored based on code efficiency (hint: use functions, not stream of consciousness coding), code cleaniless, code reproducibility, and critical thinking (hint: commenting lets me know what you are thinking!)
Instructions:

	Submit the following 5 items on github.
	ReadMe.md (see "Critical Thinking")
	requirements.txt
	pull_data.py
	train_model.py
	score_model.py

More details:

requirements.txt (1 point)
This file documents all dependencies needed on top of the existing packages in the Docker Dataquest image from HW1. When called upon using pip install -r requirements.txt , this will install all python packages needed to run the .py files. (hint: use pip freeze to generate the .txt file)

pull_data.py (5 points)
When this is called using python pull_data.py in the command line, this will go to the 2 Kaggle urls provided below, authenticate using your own Kaggle sign on, pull the two datasets, and save as .csv files in the current local directory. The authentication login details (aka secrets) need to be in a hidden folder (hint: use .gitignore). There must be a data check step to ensure the data has been pulled correctly and clear commenting and documentation for each step inside the .py file.
	Training dataset url: https://www.kaggle.com/c/titanic/download/train.csv
	Scoring dataset url: https://www.kaggle.com/c/titanic/download/test.csv

train_model.py (5 points)
When this is called using python train_model.py in the command line, this will take in the training dataset csv, perform the necessary data cleaning and imputation, and fit a classification model to the dependent Y. There must be data check steps and clear commenting for each step inside the .py file. The output for running this file is the random forest model saved as a .pkl file in the local directory. Remember that the thought process and decision for why you chose the final model must be clearly documented in this section.
eda.ipynb (0 points)

[Optional] This supplements the commenting inside train_model.py. This is the place to provide scratch work and plots to convince me why you did certain data imputations and manipulations inside the train_model.py file.

score_model.py (2 points)
When this is called using python score_model.py in the command line, this will ingest the .pkl random forest file and apply the model to the locally saved scoring dataset csv. There must be data check steps and clear commenting for each step inside the .py file. The output for running this file is a csv file with the predicted score, as well as a png or text file output that contains the model accuracy report (e.g. sklearn's classification report or any other way of model evaluation).

3. Critical Thinking (2 points total)
Modify this ReadMe file to answer the following questions directly in place.<br>

> 1) Kaggle changes links/ file locations/login process/ file content

  The code should be able to handle this kind of changes, meaning that there should be one place that holds the URLs/credentials/file names (if too many) to feed into the function to download the datasets. In this project's case, REST calls are done to Kaggle APIs and takes in from console the username/password. At any point and time, the code should handle errors whether URL, login or dataset contents. The error should indicate what's happening and nased on that to address a fix for it.
  <br>

> 2) We run out of space on HD / local permissions issue - can't save files

  Based on the size of the datasets working with and taking into the consideration the code compile time and runtime, if this will exhaust the local machine then an alternative ways are needed to be used, for example:

  - create and save content in files stored in external HD
  - dockerize your application
  - deploy your code, datasets and generated files into the servers/cloud environments

  In case of permission issues, it's better to use SSL certificates and throw errors if cert file is not there or if permission is not verified, etc.
  <br>

> 3) Someone updated python packages and there is unintended effect (functions retired or act differently)

  The code should be bound with error catchers, with excepts and other forms of error handling methods. Tagging with docker images can help revert to a specific version when there's an error with the latest version or the deployed version for packages within the application. If community packages, then there should be a way in the code design to notice this behavior.
  <br>

> 4) Docker issues - lost internet within docker due to some ip binding to vm or local routing issues( I guess this falls under lost internet, but I am talking more if docker is the cause rather then ISP)

  There are multiple ways to target fixes to issues with docker based on each issue situation. To best handle docker behaviors, we can:

  - check the containers list for missing or failed docker containers (ignoring latency for now)
  - use event handler that will remove a NAT rule or node listeners if consul is setup to get notified about failures  or clear state of a container through reboot

Team 01 : Aspect and Opinion Extraction for Amazon Reviews
===========================================================

What is this?
-------------
This is a compilation of all the things required to run this project file.
It is arranged in a step-wise manner, where we cover setting up the environment first,
explain the different code files and finally how to run the visualisation.

Github link - https://github.com/ishikaarora4/Aspect-Sentiment-Analysis-on-Amazon-Reviews

The folder structure of the package is mentioned below -
/data - Contains all the required data files
/src - Contains all the code files
/UI - Contains the required files for seeing the Visualisation
requirements.txt - File to setup the python environment for running the model  [NEED TO UPDATE!!!]


Setting up the environment
--------------------------
* Setup a base python environment using Miniconda (https://conda.io/miniconda.html)
* Create a conda environment using the requirements.txt file so that all dependancies are installed
`conda create --name <env> --file requirements.txt`
* Activate the environment just created using `source activate <env_name>`
* Run this to download the language corpus we used - python -m spacy download en_core_web_lg
* Run this to download the NLTK polarity model inside a python shell - nltk.download('vader_lexicon')


Note : The models take upto 7-8hours to run for 1M set of reviews. We ran the whole process on
an AWS EC2 instance. Moreover, roughly the loading of NLP language corpus itself needs around
2GB RAM, so use higher configurations. We used


Code Files
----------

/src/dataprep/clean_data.py - Contains function to clean the review text
/src/dataprep/aspect_json_encoding.py - An ad-hoc file used to solve an encoding issue when writing the file in json format

/src/models/aspect_extraction.py - Contains all the required functions to fetch the data from S3 buckets and give aspect-aspect modifier in a json format.
/src/models/mapper.py - Aggregates all the aspect-aspect modifiers according to product_id which will be passed on to the clustering script

/src/models/aspect_clustering.py - Contains all required functions to run clustering


How to run?
----------

We are providing with two options to run -
1. On one whole file (amazon_reviews_us_Electronics_v1) which has around 3M+ reviews
2. One toy file we have created as a subset of the above mentioned file

Add argument as 1, if you want to run on the toy file.

Note : Run all commands from the code folder

* python src/models/run_extraction.py <arg = 1 or 0>
* python src/models/aspect_clustering.py

About the files that are generated -
* All the files generated in data/interim folder are needed for functioning of the model.
* Files in data/processed -
  * model_results_encoding.json - the final file that is used to populate the db and then UI used it
  * reviews_aspect_mapping.json - the output file from first step (aspect extraction) used by clustering
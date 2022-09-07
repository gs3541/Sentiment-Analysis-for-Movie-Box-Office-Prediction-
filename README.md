# Sentiment-Analysis-for-Movie-Box-Office-Prediction-

Final Project Part II Readme

Class: Predictive Analytics - Summer 2022

Team Members:
(Name, netID, NYU ID)
Gurmehr Sohi, gs3541, N15515110
Caglar Dogan, cd2647, N18970424
Ekantika Singh, eas9980, N13606584

----- ----- Code Files ----- -----

The code files consist of three Jupyter Notebook files (.ipynb).

The notebook files have text segments (both as headers and explanation paragraphs) that provide context to what is done.
If any further explanation is necessary, please refer to the text sections of the notebook files.

The main information regarding each code file can be summarized as follows:

----- -----
Extraction_from_IMDB.ipynb: 
(Please be warned that this program runs for a long time (like an hour) to be able to collect all the necessary data)
(Running this code fully is not advised for this reason, although the code works.)

The code in this file scrapes the IMDB website to get information about the first 2000 feature movies (according to the IMDB popularity score) produced in the USA and available in English that were released between 2016-01-01 and 2019-12-31.

The first 2000 movies were selected to reduce the time needed to gather the relevant data. We had noticed that a great majority of movies that are less popular do not contain the US opening weekend gross information - and thus are not usable for our models. For this reason, this restriction of our web scraping process to 2000 movies does not reduce the number of valid data points we get much, while it reduces the time needed to complete the process drastically.

The result is saved into a CSV file with the name "IMDB_movie_data.csv". Please note that the data in this file must be cleaned, and relevant sentiment information must be added before the use of this data in modeling.

----- -----
data_cleaning_and_sentiment.ipynb: 
(Please be warned that this program runs for a long time (like an hour) to be able to collect all the necessary data)
(Running this code fully is not advised for this reason, although the code works.)
(Please be sure to use a system that won't automatically close/disconnect after a certain period of inactivity if running this code)

The code in this file reads the "IMDB_movie_data.csv" (which contains information about the first 2000 feature movies (according to the IMDB popularity score) in IMDB produced in the USA and available in English that were released between 2016-01-01 and 2019-12-31), applies pre-processing by converting the string features into forms directly usable in our models and cleans the data, and gathers the needed sentiment information metrics for each movie.

During this process, an intermediate CSV file with the name "clean_data.csv" is generated, which includes cleaned and pre-processed data without sentiment information.

The end result is saved into a CSV file with the name "model_data.csv", from where it can be read and used for further data exploration and modeling.

----- -----
models.ipynb:
The code in this file reads the "model_data.csv" (which contains the information scraped from IMDB for each movie as well as sentiment scores and a popularity score calculated from the posts in the last five days before release), provides insight into the attributes present, and trains and tests predictive models using this information.

This is the main code file to run to see model performence and data evaluations.


----- ----- Running The Code Files ----- -----

For all the files, the results of the last runs should be visible without the need to run the files again.
These pre-existing results can be specifically usefull for the "Extraction_from_IMDB.ipynb" and "data_cleaning_and_sentiment.ipynb" files.

However, if a re-run of the code is needed, it should be ensured that the correct dependencies are present in the system:
(The imports are done in the code, but these are assumed to be installed unless specified)

----- Dependencies -----

Extraction_from_IMDB.ipynb:
    numpy
    pandas
    requests
    BeautifulSoup

data_cleaning_and_sentiment.ipynb: 
    numpy
    pandas
    requests
    BeautifulSoup
    regex
    psaw (For the PushshiftAPI, installed by command in the notebook)
    datetime
    swifter (For parallelized pandas apply, installed by command in the notebook))
    nltk
    textblob

    Please note that this file includes the following download and setup commands:
        !pip install psaw

        !pip install -U pandas # upgrade pandas
        !pip install swifter # first time installation
        !pip install swifter[groupby] # first time installation including dependency for groupby.apply functionality

        !pip install -U swifter # upgrade to latest version if already installed
        !pip install -U swifter[groupby] # upgrade to latest version to include dependency for gr

        !pip install flair

        After importing nltk:
            nltk.download('vader_lexicon')
            nltk.download('punkt')

models.ipynb:
    numpy
    pandas
    statistics
    sklearn
    matplotlib

When the dependencies are present, simply using Jupyter Notebooks to open the files and run all the cells should be enough.

All the code files were run on Colaboratory - Google Research (https://colab.research.google.com), and should work with Jupyter Notebook setups compatible with the dependency versions of Google Colaboratory.

----- ----- Data Files ----- -----

The data files consist of three CSV files - each representing a Pandas DataFrame.

IMDB_movie_data.csv:
This file contains the movie information scraped from the IMDB website and is generated by "Extraction_from_IMDB.ipynb".

clean_data.csv:
This file contains the cleaned information from IMDB_movie_data.csv. 
This file is written and read by "data_cleaning_and_sentiment.ipynb" and acts as intermediary storage.

model_data.csv:
This file contains the cleaned and merged IMDB movie information and Reddit sentiment information.
This file is read and used by "models.ipynb" for data exploration, modeling, and evaluation.

Please note that the code files "Extraction_from_IMDB.ipynb" and "data_cleaning_and_sentiment.ipynb" generate these data files (with data from web scraping and API accesses).
Thus, if any changes are made to the code and the code is only half-executed/fails, there might be changes to these data files.
For this reason, please always refer to the original files and keep a copy if the data generation code will be run.

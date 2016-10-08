# Setting up

* Install [Annaconda](https://www.continuum.io/downloads)

# Running

* First Download the data, its [here](https://www.kaggle.com/wcukierski/the-simpsons-by-the-data)
* Then extract the scripts, using [ExtractScripts.ipynb](ExtractScripts.ipynb)
* Then concatenate together into a single file `cat episodes_data/* > simpsons_data.txt`

* Then train the model in a docker container (taken from [here](https://github.com/crisbal/docker-torch-rnn))
* Run `docker build -t simpsonnet .`
* This will build the docker container, and the model!

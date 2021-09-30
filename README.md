# NLP_Text_Generation

This project generates lyrics/songs from this [dataset](https://www.kaggle.com/neisse/scrapped-lyrics-from-6-genres) . The library ([torch-rnn](https://github.com/jcjohnson/torch-rnn)) trains character level language models based on multu-layer LSTMs. This is based on torch7.

--------------

# Steps to Generate the Songs
* After trying to install torch7 on Mac (M1) and Ubuntu (20.04), I've realised torch7 is not fully compatible with these yet. You can run the docker image to ease all the pain (Don't run in M1). Download the [Docker](https://www.docker.com/get-started) if not installed yet.
* Connect to the docer bash in the container
```
docker run --rm -ti crisbal/torch-rnn:base bash 
```
* Download the dataset into the docer container
```
curl https://raw.githubusercontent.com/AsifKibria/NLP_Text_Generation/main/Data/input.txt -o data/lyrics.txt 
```
* Preprocess the lyrics
```
python scripts/preprocess.py --input_txt data/lyrics.txt --output_h5 data/lyrics.h5 --output_json ${PREFIX}.json
```
This will create two output files in the `data` directory. You can also check all the available flags for the preprocessing [here](https://github.com/jcjohnson/torch-rnn/blob/master/doc/flags.md#training).
* Train the Model
```
th train.lua -input_h5 data/lyrics.h5  -input_json -input_json data/lyrics.json -gpu -1
```
You can also check all the available flags for the preprocessing [here](https://github.com/jcjohnson/torch-rnn/blob/master/doc/flags.md#training). Grab a coffe or have your dinner, This will take a very long time. 
* Sampling/Generating
```
th sample.lua -checkpoint cv/checkpoint_83000.t7 -length 600
```
This will generate 600 characters long new text. You can also check all the available flags for the sample [here](https://github.com/jcjohnson/torch-rnn/blob/master/doc/flags.md#training).


# NLP_Text_Generation

This project generates lyrics/songs from this [dataset](https://www.kaggle.com/neisse/scrapped-lyrics-from-6-genres). I've processed the data and trimmed it to ~5000 songs. Detailed processing and trimming process can be found in this [notebook](https://github.com/AsifKibria/NLP_Text_Generation/blob/main/Data_Preprocessing.ipynb). This .pdf version of the notebook is [here](https://github.com/AsifKibria/NLP_Text_Generation/blob/main/Data_Preprocessing.pdf). I've used pandas, numpy and Seaborn to cleaning the data. 
The library ([torch-rnn](https://github.com/jcjohnson/torch-rnn)) trains character level language models based on multu-layer LSTMs. This is based on torch7. Detailed of the technology and process can be found in the [Project Report](https://github.com/AsifKibria/NLP_Text_Generation/blob/main/NLP_Text_Generation_Project_Report_Draft.pdf). 

------------

This has been done for the Coursework of Natural Language Processing taken by [Univ.-Prof. Dr. Arthur M. Jacobs](https://www.ewi-psy.fu-berlin.de/einrichtungen/arbeitsbereiche/allgpsy/mitarbeiter_innen/ajacobs/index.html) at Freie University Berlin.

--------------

# Steps to Generate the Songs
* After trying to install torch7 on Mac (M1) and Ubuntu (20.04), I've realised torch7 is not fully compatible with these yet. You can run the docker image to ease all the pain (Don't run in M1). Download the [Docker](https://www.docker.com/get-started) if it is not in your machine.

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
python scripts/preprocess.py --input_txt data/lyrics.txt --output_h5 data/lyrics.h5 --output_json data/lyrics.json
```
This will create two output files in the `data` directory. You can also check all the available flags for the preprocessing [here](https://github.com/jcjohnson/torch-rnn/blob/master/doc/flags.md#training).

* Train the Model
```
th train.lua -input_h5 data/lyrics.h5  -input_json data/lyrics.json -gpu -1
```
You can also check all the available flags for the preprocessing [here](https://github.com/jcjohnson/torch-rnn/blob/master/doc/flags.md#training). Grab a coffe or have your dinner, This will take a very long time. 

* Sampling/Generating
```
th sample.lua -checkpoint cv/checkpoint_83000.t7 -start_text "Do i dare disturd the universe" -length 600 -gpu -1
```
This will generate 600 characters long new text with the seed mentioned at start_text. You can also check all the available flags for the sample [here](https://github.com/jcjohnson/torch-rnn/blob/master/doc/flags.md#training).

--------------
# Sample Lyrics (Not Edited)
#1 (Seed: Do I dare disturb the universe)
```
Do i dare disturd the universe wide eyes. 
Break at you when everything. 
Heart this day, yeah yeah, new mountate that wings. 
And I ain't so replaced of lime. 
Sinces was a gross "Repeat is Jenge??. 
Caubles it's the clear, show felt, tied and wake  crumper.
Elevil ale so cold home. Where did me since ever and you all find. 
Maiden arms or running. Their eyes ¬¥sorta may crazy dies. 
These cold mirror shit looks ya. 
No red and you'll. 
From real. on the closed with your dead. 
I got song. 
This is off a perfect.
Oh sky alone to spoke, But now it's only.
Behat I'm just one. 
When hook out of more half day. 
You're stare to prensemmer. 
Forgotten is precity. 
I'm pleasure land woman like a dop. Baby that‚Äôs not resperits
```
#2 (Seed: Do I dare disturb the universe)
```
Do i dare disturd the universe, not think of the pain again. 
To nothing to find out! hen - barely. What she made me days gonne On. 
You're not over and, your side.
We'll know what your heart. 
But I want to throw our bed. 
Just a small. Avoids is down it.
Do me a punk havin' me watch. 
Slildromite gays. There's a party man chack you tonight. 
Buying race of La, The Wackest,. 
And I useigin I'm tired. to say the best alone. And hard to take your faster, he floor,.
I find you go up town. Too much longer girl. Let go down the world.  Don't listen.
```
#3 (Seed: Love)
```
Love to be alone, I'm head you so feeling cared attage. 
Over me of all your tomorrow on. You've been again acroll last side. 
Lost elections come true goes. To be broken nightmare. 
Oh my hard. Promise you needle emang dream. we ain't getting learning at the heart. 
I'll find yourself until that you waste. 
Get out there's a mikuntary. Before it mercy. 
I'm not the jack. My letter, beauty was between knew.
Running you roll and got no sickly. 
I'm not control. Ooh own pessivis start. 
Sew sailtured holy fate. Take it to me to the truth that I just pull the stars.
```
#4 (Seed: Love)
```
Love Spy glocks of a front of air wheel. Caught up watch for getting. 
It's coming. I'd let me follow me home. How do I carry around. 
and your crying sense of here, baby. And I won't be all this day. 
What takes you running. Goes a done darlin'. 
we're the path Children balling. 
Surroigined, I'm like one outside.
And you're not another biet. Don't need a mether greez. 
We, we'll hold off my reason and stance. 
Yes down I'll tried for sorry. Sinch of a hopical lives.
You and those are ronnisite step.
You all shot like deach you understand. How more never a little.
```
You can also download all the trained models from [here](https://github.com/AsifKibria/nlp_torch_rnn_cv). 

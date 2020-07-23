# Generating band names with Keras

Welcome to musicnames-RNN-keras. This is a fun project I started on my own, to put together two of my passions: programming :floppy_disk: and music :notes:. 

Recently I have been learning (through deeplearning.ai, at Coursera) about deep learning, artificial intelligence, etc, and I've become quite invested in those topics. In order to challenge myself I tried to come up with a project so that I could start from the bottom up, ending with a (functional?) model. 

### The idea

My initial idea was to generate music based on my own collection of .mp3 files. However after a quick Internet search I discovered it would be a nightmare, starting from the fact that unless the music is in MIDI format, it is very hard to handle such data. I then turned to an example from the course "Sequence Models" on Coursera, the fifth and last of the series, which involved creating a dinosaur-name generator. However it did not use deep learning frameworks (Keras, PyTorch...) so I decided to do it myself, but with a different dataset: musicians. I found such dataset at [kaggle dataset](https://www.kaggle.com/pieca111/music-artists-popularity).

### The dataset

The dataset could not be imported as is, it contains way more information than the one needed for this project*, therefore some pre-processing was required. Not only that, the list had to be cleaned further, so as to dismiss unnecessarily complicated training examples (those containing punctuation signs, those containing non-latin characters, etc). More pre-processing was needed to make it suitable for Keras (i.e. conversion to one-hot vectors).


*In fact, uploading the dataset to GitHub gave me some headaches: it being larger than 100 MBs required using the Git LFS extension before pushing it to GitHub, however I was not aware of it until I was many commits ahead, therefore I had to resort to trickery and black magic (i.e. deleting the file from all previous commits using some help from the Internet) to make everything suitable for a good push.

### The structure of the repo

#### v1.1
Addition of a `variables` directory, where some useful variables (index_to_char, char_to_index, m, max_char, numchars, validchars) are saved in their corresponding files using the python Pickle module.

#### v1.0
The repository consist of the following
* This `README.md` file
* Original dataset, `artists.csv`
* `.gitattributes` file, needed in order to upload the `artists.csv` file using `git lfs`.
* Jupyter notebook, `miusic.ipynb`, containing the program
* Two directories
	* `checkpoints`: containing the weights obtained during the training, should one want to resume the training using them
	* `clearlists`: containing the four different sets of names available for training
		1. `clearedlist1.csv` contains all names without other alphabet's characters.
		2. `clearedlist2.csv`, the same as `clearedlist1.csv` but without punctuation characters and digits.
		3. `clearedlist3.csv`, the same as `clearedlist2.csv` but restricted to two-word names.
		4. `clearedlist4.csv`, the same as `clearedlist3.csv` but restricted to single word names.

### The Model

#### v1.0
I've implemented the most vanilla version of an RNN, a good-old LSTM layer followed by a Dense layer, both within a Sequential() model. There are some nuances added to the mix, such as two Keras callbacks.

The model is definitely not great, and I will be improving it whenever I find time I want to spend on this project. For instance, there is a huge margin for improvement in modifying the structure of the neural network, I have some ideas about it. This links with the next section... 

### The goals?

Besides the fun of the project, a target I had in mind which I have yet to reach is making the neural network learn that LOTS of groups with more than one word in their name include a "The" at the beginning. It's almost a default option for the first word, in my opinion. We'll see if this can be reproduced.



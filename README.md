# RP_extract:
## Rhythm Pattern Audio Feature Extractor
for Music Similarity, Music Classification and Music Recommendation

created by:

TU Wien<br>
[Music Information Retrieval Group](http://ifs.tuwien.ac.at/mir)<br>
Institute of Software Technology and Interactive Systems<br>
Vienna University of Technology, Austria

Main Authors: Thomas Lidy (audiofeature), Alexander Schindler (slychief)


## Easy Getting Started

Analyze all audio files in a folder and store the extracted features:

```
python rp_extract_batch.py <input_path> <feature_file_name>
```

This will
- search for MP3 or WAV files in input_path
- extract a standard set of audio features (RP, SSD, RH - see http://ifs.tuwien.ac.at/mir/audiofeatureextraction.html )
- write them in a CSV like manner to feature_file_name (one for each feature type: .rp, .ssd, .rh)

Optionally specify the type of features you want:

```
python rp_extract_batch.py -rp -mvd -tssd <input_path> <feature_file_name>
```

Use the following to get a list of possible feature options:

```
python rp_extract_batch.py -h
```

## Use RP_extract in your code

rp_extract.py is the main feature extractor.
It can be imported and used in your code to do segment-level audio feature analysis.

For a step-by-step tutorial open „RP_extract Tutorial.ipynb“ in iPython Notebook or view the tutorial here:

http://nbviewer.ipython.org/github/tuwien-musicir/rp_extract/blob/master/RP_extract_Tutorial.ipynb

It also includes examples on how to compute music similarity, e.g. for music recommendation or
creating playlists of coherent music.

## Genre Recognition and Classification

`rp_classify.py` will analyze audio files and categorize them into a high-level concept (such as genre, style or mood)
given a pre-trained classifier model that was created based on training data.

It can be used on a single audio file (wav or mp3) to recognize its genre like this:

```
python rp_classify.py music/BoxCat_Games_-_10_-_Epic_Song.mp3
```

will output:

```
music/BoxCat_Games_-_10_-_Epic_Song.mp3:	pop
```

You can also use a folder as an input, to analyze and predict all wav and mp3 files contained. The full syntax is:

```
python rp_classify.py input_path model_file output_filename
```

`input_path` can be: a folder, wav or mp3 file, or txt file containing a line-wise list of wav or mp3 files

The pre-trained model included in this code repository (`models/GTZAN`) can predict these 10 genres:
blues, classical, country, disco, hiphop, jazz, metal, pop, reggae, rock

`output_filename` is an optional file in which predictions will be written in a tab-separated way
(if omitted, result will be printed to stdout).


### Train a model:

You can train your own model like this:

```
python rp_classify.py -t input_path model_file
```

In this case files from `input_path` will be read and analyzed and a model will be trained and stored in `model_file`.

_Note_: For training a model, files in `input_path` must be organized in sub-folders which are named after the categories to be trained.
 (this limitation/requirement might be relieved in future through the provision of groundtruth class files)

Once you trained a model, you can do predictions given the syntax above (without the `-t` parameter).


## More Information

http://ifs.tuwien.ac.at/mir

http://ifs.tuwien.ac.at/mir/downloads.html
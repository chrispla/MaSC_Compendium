# Arab Mashriq Music Compendium

## Introduction

The Arab Mashriq Music Compendium is a digital compendium of music from the Arab Mashriq containg commercial music and unreleased field recordings. It is currently under development by the Music and Sound Cultures (MaSC) research group at NYU Abu Dhabi in collaboration with the Music and Audio Research Lab (MARL) at NYU New York and with the Centre de Recherche en Ethnomusicologie (CREM) in Paris through a Global Seed Fund Grant for project "Creation and Analysis of a Digital Repository of Middle Eastern Music".

## Metadata

Metadata are provided as a [pandas](https://pandas.pydata.org/docs/) DataFrame, which is provided in HDF5 file format as a PyTables Table structure. The `metadata.h5` file can be loaded using the `pandas.read_hdf` method.
```python
import pandas as pd
metadata = pd.read_hdf("metadata.h5")
```

Not all metadata are available for all recordings, and this is the purpose of specific datasets, as explained later in this document. Empty entries contain the keyword **None**. The metatags are listed below.
* `unique_id`
* `sample_tag_1`
* `sample_tag_2`
* `sample_tag_3`
* `sample_tag_4`
*  ...

Each recording is associated with a unique identifier that is used for retrieving the features of the recording as explained in the **Features** section.

## Features

Features are provided as a python dictionary using the unique identifiers of the recordings as keys. The `features.h5` file can be loaded using a library such as [deepdish](https://deepdish.readthedocs.io/en/latest/) with the `io.load` method.
```python
import deepdish as dd
features = dd.io.load("features.h5")
```
The `unique_id` for each recording is present in the metadata file, and can also be useful for retrieving the audio files of the collection if the user has access to them. The value of each key is a dictionary of features. The string keys for the features provided are
* `mfcc` : [Mel-frequency Cepstral Coefficients](https://librosa.org/doc/main/generated/librosa.feature.mfcc.html)
* `chromagram` : [Chromagram](https://librosa.org/doc/main/generated/librosa.feature.chroma_stft.html)
* `tempogram` : [Tempogram](https://librosa.org/doc/main/generated/librosa.feature.tempogram.html)

All features were computed using [librosa](https://librosa.org/doc/main/index.html) with the default parameters for each method. 

Below is an example of the features dictionary.
```python
{
  "0014fd26-ddbc-51e8-97db-2889829f88c9": {  # unique_id
    "mfcc": np.ndarray,  # shape=(20, t)
    "chromagram": np.ndarray,  # shape=(12, t)
    "tempogram": np.ndarray  # shape=(384, n)
   }
   ..
}
```


## Datasets

Datasets containing subsets of the collection are provided to ensure the completness of the relevant metadata for particular tasks. For each dataset, a .txt file with <em>newline</em>-separated entries is provided containing the unique identifiers of the recordings in the dataset. The file can be loaded as a python list and used to retrieve the relevant metadata and features.








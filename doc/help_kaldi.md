#Read/write kaldi features

#Read kaldi features

##Raw Feature location

Most kaldi features are stored in mfcc folder with an extension of ark or scp.

###The ark file

The ark stores raw features, its size of ark is normally in few hundred MBs.

Eg: 20 dimensional MFCC features matrix is stored in the ark file like following:

UtteranceID1 [d1 d2 d3 d4 d5 .. d20\n d1 d2 d3 d4 d5 .. d20\n d1 d2 d3 d4 d5 .. d20\n ...]\n

UtteranceID2 [d1 d2 d3 d4 d5 .. d20\n d1 d2 d3 d4 d5 .. d20\n ]\n

Where \n means new line.

To view raw feature, type the following command in the terminal
```
copy-feats ark:./abc.ark ark,t:
```
This command means copy the feature form input source (ark:source) to output target (ark,t:target),here we leave "target" empty so the feature will print to the terminal.
Following two commands will dump the features to text file
```
copy-feats ark:./abc.ark ark,t: > a.txt
copy-feats ark:./abc.ark ark,t:a.txt
```
And dump to binary file:
```
copy-feats ark:./abc.ark ark:a.bin
```


###The scp file

It is often saw a scp file with the same file name which describes the content of an ark file.

The scp is only a text file, with following format:

UtteranceID1 arkLocation1:offset1 

UtteranceID2 arkLocation2:offset2




Following two commands will give same results
```
copy-feats scp:./abc.scp ark,t:
copy-feats ark:./abc.ark ark,t:
```
##Features in the data folder

feats.scp and vad.scp are two feature descriptors in the Kaldi data folder.


#write kaldi features

One can write kaldi feature to the ark follow the given text format. However most script in kaldi requre its scp file, one way to create scp file is:
```
copy-feats ark:./abc.ark ark,scp:b.ark,b.scp
```
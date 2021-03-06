##pylexemes by Anton Osten

Currently a reconstructor of proto-forms. More features may be coming in future.

# DISCLAIMER
The author of this program takes no responsibility for its behaviour and possible unfavourable consequences. While no such functionality was intended, it is not within the realm of impossibility that in the course of its running this code will fail, make your computer freeze up or burn down, or open a portal to a hostile alien world in a distant galaxy.

Additionally, please be aware that due to the experimental and therefore highly unstable nature of this project, I may update or delete any part of its code daily in the hope of making it work better, but quite possibly making it worse.

# Disclaimer for linguists
While this program may produce interesting results, it is first and foremost a toy, and therefore should not be viewed particularly seriously, and certainly should not be trusted to produce accurate results. While I am eager to make it as accurate as I am, I highly doubt that I will be able to produce a tool which would make comparative method done with humans 'by hand' redundant, certainly not at this point. This started as a project for my CompSci class, and at this point in time has not really transcended that status by much.

Feel free to play around with it, and laugh at the results it produces (we, linguists, are a notoriosuly humorous folk), but please don't email me saying that it sucks, since I pretty much know that anyway. If, however, you have useful (and concrete) suggestions on how to improve the algorithm(s) to make it work better, and you wish to share those with me, please do so. 

Additionally, if you can think of a way that this could be adapted into something that would be useful in real-world linguistics (*sad laughter*), please don't hesitate to contact me as well.

# System requirements
Any machine running Python 3. Although this was written and tested only on OS X 10.8, it should work on any other UNIX systems and possibly even Windows as-is.

# Necessary files:
- segmentparser.py
- lexemeparser.py
- segments.json
- lexemes.json (a dummy is generated by lexemeparser.py if it's not found)
- reconstructor.py

# How to use
The program comes provided with a phoneme database in JSON format, which contains for each phoneme its IPA symbol, its name, and a feature set of (currently) up to 22 binary features.

To reconstruct a theoretical proto-form, you need to input a set of lexemes which you believe to be cognates into the lexemes.json file (one should come provided for reference), and then run the reconstructor.py script. 

# How it works
reconstructor.py takes a set of lexemes given to it by lexemeparser.py from the lexemes.json file and deconstructs each of those lexemes into individual IPA symbols and places them into groups according to their position in the lexemes. It then replaces each such symbol with its feature representation as provided by the phonemes.json file, and then deconstructs each phoneme-as-feature-set into individual features. It then takes each such individual feature from each phoneme group and from all features of all the phonemes in the group assembles what I call a theoretical phoneme, containing most frequent features of each phoneme in that group (yes, I know that frequency is not the best way to assemble those features in terms of actual comparative method). 

After that, it takes each 'theoretical phoneme' and tries to find a match for it in the database to get its IPA symbol. If there is no match, the program finds whichever phoneme has the feature set most similar to the theoretical phoneme (using similarity ratio from difflib.SequenceMatcher), and plugs that in its place, doing so in brackets to indicate that it was a guess.

# Contact me
anton@ostensible.me
---------------------------------------------
# Version history

## v 0.6
- Branch collapsing didn't work out. In some cases it led to better results, but actually because of its bugs. Yeah. I'll keep in a separate branch, and will come back to it if I have an epiphany, but otherwise it's a failed experiment :(
- On a happier note, I am not giving up totally, and will try to implement some amount of self-learning. We'll see how that works out.

## v 0.5.5 notes (6 Feb 2013):
- Structural changes: reconstructor is now a class, Reconstructor. Phonemes are now called **segments,** which they should've been from the start. Thanks to Rafael.
- Reconstructor now has what I call branch-collapsing, whereby it selects the two most similar branches (based on the deconstructed features of their invididual phonemes) and collapses them into one, and then the next two (but not necessarily the on that was just collapsed), and so on. In theory, this should lead to more accurate results, as it should at simulate going up the tree at least somewhat. In practice, it can lead to all sorts of crazy stuff, which is why the old, non-branch-collapsed result is still provided at the end.
- It was even worse until I made the deconstruction operate based on average and not maximum form length (because all that extra junk morphology was tacked on at the end), and introduced a similarity threshold between forms, which is currently based on the average similarity of the initial forms.
- Errors corrected in the segment database.
- Bugs fixed, bugs created.

##v 0.5 notes (4 Feb 2013):
- I skipped 0.4 because I felt like it.
- reconstructor.py is *even more intelligent* now (which is still not that intelligent). It can try to rearrange the phoneme groups so that each phoneme is in the group that it belongs to, using similarity ratios, and it can also use similarity ratios to make an educated guess for a theoretical phoneme if it can't find an exact match in the database.
- Fixed occasional mistakes in phonemes.json and some stupidity in phonemelookup.py.
- The readme should be pretty comprehensive now.

##v 0.3.5 notes (3 Feb 2013):
- added phonemelookup.py, which is basically an interface for the phoneme database. You can search for phoneme IPA symbols, names, or features. It's pretty cool.

##v 0.3 notes (31 Jan 2013):
- reconstructor.py now has variable levels of verbosity (maximum 3, by default 0) acessible through the -v or -verbose commands. It can also create an ongoing log (-l or -log) of reconstructions, as per the verbosity level specified.

##v 0.3a notes (30 Jan 2013):
- reconstructor.py can now correctly behave if it is fed forms containing phonemes which are represented by more than one symbol (affricates, labialised, palatilised, etc. consonants).
- Most of the phonemes database has been fully rewritten so that each phoneme is represented by binary features, up to 22 features for each phoneme. This is a big step forward, as it enables much greater accuracy, as well as consistency in the phoneme database.

##v 0.2.5 notes (22 Jan 2013):
- removed the division into consonants and vowels in phonemes.json. That was stupid and made my life more complicated than it had to be. I have no idea why my brain decided it would be a good idea in the first place. Everything should be a bit simpler and more elegant now.
- reconstructor.py can do minimal (read: practically no) guessing of theoretical phonemes that are unmatched. I'll work on it more later.
- I am considering switching to Townsend-Janda phoneme feature notation because it seems like it would work better than the normal one.

##v 0.2.1.1 notes (21 Jan 2013):
- better error handling in lexemeparser and phonemeparser

##v 0.2.1 notes (21 Jan 2013):
- modified lexemeparser.py to create a dummy lexemes.json file if one isn't there for whatever reason

##v 0.2 notes (21 Jan 2013):
- Complete rewrite
- Now using json instead of XML to make it less bulky and faster (hopefully)
- Still only 1:1 matches and no support for aspiration, nasalisation, labialisation, ejectives, affricates, and many other things

##v 0.1 notes:
- Initial version


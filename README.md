<h1 align="center">
  <br>
  <a href="http://thalesbertaglia.com/enelvo"><img src="https://github.com/tfcbertaglia/enelvo/raw/master/enelvo-logo.png" alt="Enelvo" width="400"></a>
</h1>

<h4 align="center">A flexible normaliser for user-generated content in Portuguese.</h4>
Enelvo is a tool for normalising noisy words in user-generated content written in Portuguese -- such as tweets, blog posts, and product reviews. It is capable of identifying and normalising spelling mistakes, internet slang, acronyms, proper nouns, and others.

The tool was developed as part of my master's project. You can find more details about how it works in my [dissertation](http://www.teses.usp.br/teses/disponiveis/55/55134/tde-10112017-170919/en.php) (in Portuguese) or in [this paper](http://anthology.aclweb.org/W/W16/W16-3916.pdf) (in English). For more information in Portuguese, please visit the [project website](http://thalesbertaglia.com/enelvo).

## Getting Started
To clone and run this application, you'll need [Git](https://git-scm.com) and [Python>=3.5](https://www.python.org/) installed on your computer. First of all, download the repository as a ZIP or run from your command line:

```bash
# Clone this repository
$ git clone https://github.com/tfcbertaglia/enelvo.git

# Go into the repository
$ cd enelvo
```

## Installing
Make sure you have all dependencies installed. You also need to have Cython properly installed, follow the instructions [here](http://cython.readthedocs.io/en/latest/src/quickstart/install.html). If you use [pip](https://pypi.python.org/pypi/pip), simply run ``pip install --user -r requirements.txt``.

After that, run `python3 setup.py install` to install Enelvo.

To make sure that the installation was successful, run:
```bash
python3 -m enelvo --input in.txt --output out.txt
```

If eveything went correctly, ``out.txt`` will be written -- containing the normalised version of ``in.txt``.

## Running
You can use the tool, with the most simple configuration, by running:
```bash
python3 -m enelvo --input in.txt --output out.txt
```

There are two **required** arguments: ``--input`` (path to the input file) and ``--output`` (path+file name to which Enelvo will write the output). Enelvo considers that each line in the input file is a sentence, so format it accordingly. Use option ``-h`` to see the full list of arguments and their explanation.

You can also run Enelvo in **interactive mode**. In this case, you will be able to type in sentences and their normalised version will be displayed in real-time. To use interactive mode, just run:
```bash
python3 -m enelvo --interactive
```

Each of the arguments and their usage will be explained in the following section.

## Arguments
There are some arguments that allow you to personalise how Enelvo works. You can find the details by adding ``-h`` or ``--help`` when running the tool or by reading the sections below.

### Changing the Lexicon
Argument ``-l`` or ``--lex`` lets you choose the lexicon of words considered correct -- i.e, this argument sets the language dictionary. The input must be the full file path (e.g. ``../some/folder/dict-pt.txt``).

### Ignore and Force Lists
Unfortunately, the language lexicons we use are not perfect. Sometimes they contain words that are not in fact correct, therefore preventing them from being normalised. They also sometimes don't contain words that are correct, thus wrongly marking them as noise.
In order to ease this problem, Enelvo implements **ignore** and **force** lists.

An ignore list is a list of words that will *always* be considered **correct** -- even if not contained in the language lexicon. To use it, add ``-iglst path_to_list`` or ``-ignore-list path_to_list``. The input must be the full path file and the file must contain a single word per line.

A force list is a list of words that will *always* be considered **noisy** -- even if contained in the language lexicon. Thus, these words will alway be normalised. To use it, add ``-fclst path_to_list`` or ``-force-list path_to_list``. The input must be the full path file and the file must contain a single word per line.

### Changing the Tokeniser
By default, the tokeniser used in Enelvo replaces some entities with pre-defined tags. Twitter usernames become ``USERNAME``, numbers (including dates, phone numbers etc) -> ``NUMBER``, URLs -> ``URL``, Twitter hashtags -> ``HASHTAG``, emojis -> ``EMOJI`` etc.

If you want to keep the tokens as they are (so no replacement tags), use ``-t readable`` or ``--tokenizer readable``.

### Capitalising Entities
Enelvo can capitalise different entities using lexicons. In order to do so, you just need to set a flag for each entity that you want to capitalise.

To capitalise proper nouns, set ``-cpns`` or ``--capitalize-pns``.

To capitalise acronyms, set ``-cacs`` or ``--capitalize-acs``.

To capitalise initials (first letter after punctuation or at the beggining of a sentence), set ``-cinis`` or ``--capitalize-inis``.

### Cleaning the Text
Enelvo also provides some methods for "cleaning" the text. If you want to remove punctuation, emojis, and emoticons from all sentences, simply set ``-sn``or ``--sanitize``.

### Other Arguments
There are some other arguments used to control the internal functioning of the normalisation methods (like thresholds etc). Use ``-h`` or ``--help`` to see further details.

## What Else?
Everything described here is related to using Enelvo as a *tool*. However, it can be personalised and configured way further when used as an API. It is possible to generate and score candidates using a lot of different metrics and methods -- you can even use your own metrics! Have a look at ``__main__.py`` to understand how to start. The code is reasonably well-commented, so it shouldn't be too difficult to understand what is happening.

If you have any questions, comments, suggestions or problems with Enelvo, please feel free to [contact me](http://thalesbertaglia.com).

## Acknowledgements
Many people were fundamental in carrying out this project (and my master's in general), so I would like to thank some of them.

Huge thanks to Graça Nunes, Henrico Brum, Rafael Martins, Raphael Silva, and Thiago Pardo, who devoted a (big) portion of their valuable time to annotate the corpus that served as the basis for this project.

Thanks to Marcos Treviso for helping me organise and implement many parts os this project, and for teaching me a great deal of what I know about NLP.

Thanks to all my fellow labmates from NILC for helping throughout my whole master's.

Thank you all! 😬

# BERT

BERT (Bidirectional Encoder Representations from Transformers) is a paper published by researchers at Google AI Language in October 2018. It has caused a stir in the Machine Learning community by presenting state-of-the-art results in a wide variety of NLP tasks, including Question Answering (SQuAD v1.1), Natural Language Inference (MNLI), and others. On December 9, 2019, it was reported that BERT had been adopted by Google Search for over 70 languages.

Google CLaat link: https://docs.google.com/document/d/1NwOshs-3_eBvzpP8XHsfYtCtRZhMleKM07xXQqawpwI/edit#

## Setup

**Using Colab GPU for Training**

Google Colab offers free GPUs and TPUs! Since we’ll be training a large neural network it’s best to run this ipynb file in Google Colab GPUs.

## Installing the Hugging Face Library

Install the transformers package from Hugging Face which will give us a pytorch interface for working with BERT. 

`!pip install transformers`

## Download CoLA dataset

We’ll use The Corpus of Linguistic Acceptability (CoLA) dataset for single sentence classification. It’s a set of sentences labeled as grammatically correct or incorrect. It was first published in May of 2018, and is one of the tests included in the “GLUE Benchmark” on which models like BERT are competing. The dataset is hosted on GitHub in this repo: https://nyu-mll.github.io/CoLA/

We’ll use the wget package to download the dataset to the Colab instance’s file system.

`!pip install wget`

from pathlib import Path
​
class DisplayablePath(object):
    display_filename_prefix_middle = '├──'
    display_filename_prefix_last = '└──'
    display_parent_prefix_middle = '    '
    display_parent_prefix_last = '│   '
​
    def __init__(self, path, parent_path, is_last):
        self.path = Path(str(path))
        self.parent = parent_path
        self.is_last = is_last
        if self.parent:
            self.depth = self.parent.depth + 1
        else:
            self.depth = 0
​
    @property
    def displayname(self):
        if self.path.is_dir():
            return self.path.name + '/'
        return self.path.name
​
    @classmethod
    def make_tree(cls, root, parent=None, is_last=False, criteria=None):
        root = Path(str(root))
        criteria = criteria or cls._default_criteria
​
        displayable_root = cls(root, parent, is_last)
        yield displayable_root
​
        children = sorted(list(path
                               for path in root.iterdir()
                               if criteria(path)),
                          key=lambda s: str(s).lower())
        count = 1
        for path in children:
            is_last = count == len(children)
            if path.is_dir():
                yield from cls.make_tree(path,
                                         parent=displayable_root,
                                         is_last=is_last,
                                         criteria=criteria)
            else:
                yield cls(path, displayable_root, is_last)
            count += 1
​
    @classmethod
    def _default_criteria(cls, path):
        return True
​
    @property
    def displayname(self):
        if self.path.is_dir():
            return self.path.name + '/'
        return self.path.name
​
    def displayable(self):
        if self.parent is None:
            return self.displayname
​
        _filename_prefix = (self.display_filename_prefix_last
                            if self.is_last
                            else self.display_filename_prefix_middle)
​
        parts = ['{!s} {!s}'.format(_filename_prefix,
                                    self.displayname)]
​
        parent = self.parent
        while parent and parent.parent is not None:
            parts.append(self.display_parent_prefix_middle
                         if parent.is_last
                         else self.display_parent_prefix_last)
            parent = parent.parent
​
        return ''.join(reversed(parts))
​
​
# Insert your Path here
dir_path = 'https://github.com/Sachin-NeU/BERT/edit/master/README.md'
paths = DisplayablePath.make_tree(Path(dir_path))
​
for path in paths:
    print(path.displayable())
    # find . | grep -E "(.DS_Store)" | xargs rm -rf

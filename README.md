[![Build Status](https://travis-ci.org/wtsi-hgi/python-common.svg)](https://travis-ci.org/wtsi-hgi/python-sam-header-parser)
[![codecov.io](https://codecov.io/gh/wtsi-hgi/python-sam-header-parser/graph/badge.svg)](https://codecov.io/github/wtsi-hgi/python-sam-header-parser)

# python-sam-header-parser

## Introduction
This project is useful for parsing a SAM/BAM/CRAM header in order to extract only the useful information from it.

## Prerequisits
It runs with python >= 3.5 and it need samtools > 1.3 in the PATH.

## Installation
```bash
pip3 install git+https://github.com/wtsi-hgi/python-sam-header-parser.git@<commit_id_or_branch_or_tag>#egg=sam_header_parser
```

## Usage:
- For data in iRODS:

```python
    from sam.header_extractor import IrodsSamFileHeaderExtractor, LustreSamFileHeaderExtractor
    from sam.header_parser import SAMFileHeaderParser, SAMFileRGTagParser

    header_as_text = IrodsSamFileHeaderExtractor.extract(fpath)
    raw_header = SAMFileHeaderParser.parse(header_as_text)
    rg_tags_parsed = SAMFileRGTagParser.parse(raw_header.rg_tags)
    
    # => getting the samples:
    samples = rg_tags_parsed.samples
    libraries = rg_tags_parsed.libraries
```
where samples and libraries will be each a set of strings corresponding to the ids extracted from the header.

For lustre data the only difference is the first line:

```python
    header_as_text = LustreSamFileHeaderExtractor.extract(fpath)
    # ....
```

# Introduction
The purpose of this project is to test an applicant's coding and software design abilities.
To that end, you may use online documentation and resources just as you would in your
day-to-day work.  This project is designed to be completed within a few hours.

# Project Story
Emsi has large collections of documents and performs daily ingestion of new documents.
The processing pipelines for these documents are designed to be streaming such that
only one or a few documents are in memory at a time.  You have been asked to build a
component in such a pipeline for processing job postings scraped from the Internet.
The purpose of this component is to tag each document with a Standard Occupation Code
based on the already present ONET code, compile some summary statistics on the
dataset, and reformat the data as a SQLite database.

The sample data (`sample.gz`) is gzipped JSON lines.  Each line is a JSON object describing
a job posting.  The input objects should be mapped to rows in a SQLite table with the following schema:

```
{
    body: TEXT,
    title: TEXT,
    expired: DATE,
    posted: DATE,
    state: TEXT,
    city: TEXT,
    onet: TEXT,
    soc5: TEXT,
    soc2: TEXT
}
```

Most fields should simply be copied across, with three exceptions:
* `body` should be the input `body` stripped of everything that looks like an HTML tag.
* `soc5` should be injected based on the input `onet` and the associated mapping described in `map_onet_soc.csv`.
* `soc2` should be injected based on `soc5` and the parent/child relationships
  defined in `soc_hierarchy.csv`. The occupation codes are hierarchical, and
  soc5 codes are subsets of soc2 codes. For example, 11-9000: "Other Management
  Occupations" is a parent code of 11-9020: "Construction Managers".

The summary statistics your process must calculate are these:
* Number of documents from which you successfully removed HTML tags.
* Count of documents for each `soc2`.
* Total number of postings that were active on February 1st, 2017.

# Implementation Notes
* The code can be written in the language of your choice.
* Your solution must run on Debian Stretch (linux).
* The output format should be a SQLite database. Summary stats may be printed to stdout, or documented as SQLite queries to be run on the output DB.
* While the data sample is small enough to fit easily into memory, the implementation must be streaming, assuming much larger datasets.
* Provide clear instructions for how to compile/run your code, along with any required packages that are not installed by default on Debian Stretch.
* If you find these requirements to be ambiguous, go with your best guess and document your decision.

# Submission Process
* Create a repository on Github and email us a link.
* The repository should include a README.md that clearly describes how to compile and run your code.

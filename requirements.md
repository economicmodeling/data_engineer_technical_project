# Introduction
The purpose of this project is to test an applicant's coding and software design abilities.
To that end, you may use online documentation and resources just as you would in your
 day to day work.  This project is designed to be completed within a few hours.
 
# Project Story
Emsi has large collections of documents and performs daily ingestion of new documents.
The processing pipelines for these documents are designed to be streaming such that 
only one or a few documents are memory at a time.  You have been asked to build a
component in such a pipeline for processing job postings scraped from the Internet.
The purpose of this component is to tag each document with a Standard Occupation Code
 based on the already present ONET code.
 
The sample data (`sample.gz`) is gzipped JSON lines.  Each line is a JSON object describing
a job posting.  The input objects should be mapped to lines of JSON objects with the following schema:

```
{
	body: string,
	title: string,
	expired: string,
	posted: string,
	state: string,
	city: string,
	onet: string,
	soc5: string,
}
```

Most fields should simply be copied across, with two exceptions:
* `body` should be the input `body` stripped of everything that looks like an HTML tag.
* `soc5` should be injected based on the input `onet` and the associated mapping described 
         in `map_onet_soc.csv`.  Empty or unmapped `onet` values should map to `null`.

# Implementation Notes
* The code can be written in the language of your choice.
* Your solution must run on Debian Stretch.
* While the data sample is small enough to fit easily into memory, the implementation must be streaming, assuming much larger datasets.
* Either supply a Dockerfile or provide clear instructions for how to compile and run your code, along with any non-default packages required.
* If you find these requirements to be ambiguous, go with your best guess and document your decision.

# Submission Process
* Create a repository on Github and email us a link.
* The repository should include a README.md that clearly describes how to compile and run your code.

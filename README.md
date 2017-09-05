# getting-started
How to get started with the single cell batches comparison


[TOC]: # " "

- [Motivation](#motivation)
- [Data and document access](#data-and-document-access)
- [Meetings](#meetings)
- [Data Access](#data-access)
    - [Single-cell Human BJ Fibroblasts produced by CSHL Single Cell Analysis students](#single-cell-human-bj-fibroblasts-produced-by-cshl-single-cell-analysis-students)
    - [Publicly available bulk fibroblast sequencing](#publicly-available-bulk-fibroblast-sequencing)
- [Git tutorials/Introductions](#git-tutorialsintroductions)
- [Downloading folders (aka "cloning repositories")](#downloading-folders-aka-cloning-repositories)
- [Adding an algorithm](#adding-an-algorithm)
- [Getting and Giving Help](#getting-and-giving-help)

## Motivation


The students of the
[Single Cell Analysis](https://meetings.cshl.edu/courses.aspx?course=C-SINGLE&year=17)
course at CSHL this year produced an excellent RNA-seq dataset of ~13,000
single cells produced by 6 different pairs of students (the "batch"). A
[cursory analysis](https://gist.github.com/233b00599492f4f3a333e684cb79181f) of the data, using
[PhenoGraph](https://github.com/jacoblevine/PhenoGraph) to cluster by the group
that performed the experiment, rather than completely randomly.

![cshl-singlecell-fibroblasts](cshl-singlecell-fibroblasts.png)

We aim to compare multiple batch effect correction algorithms to see if we can
remove the per-group effect.

## Data and document access


1. Fill out [this form](https://goo.gl/forms/0zVJkkl0GKjtSrCL2) with your name,
   email, and github username. After you fill that out, you should always have
   seamless access to the websites and services below. If it's not the case,
   email Olga (olga.botvinnik-youknowwhatgoeshere-czbiohub.org)
   1. Calendar events
      ([link](https://calendar.google.com/calendar/embed?src=czbiohub.org_kmsilch9cs92me1at7152fqfpo%40group.calendar.google.com&ctz=America/Los_Angeles))
      \- We meet Mondays at 9am PDT / 11am EDT
   2. Google Drive documents ([link](https://drive.google.com/open?id=0B017aFD5c7rIbG02TzNQMmM2Z2c))
   3. Amazon Web Services storage aka "AWS S3". Everything will be stored in
      the publicly viewable `s3://singlecell-batches` bucket. IF you would like
      write access, please contact Olga (olga.botvinnik@czbiohub.org)
   4. GitHub `singlecell-batches` organization
      ([link](https://github.com/singlecell-batches))
   5. Open Science Framework "Single-cell RNA-Seq Batch Effect Algorithm
      Comparison" project ([link](https://osf.io/7xm6k/))
   6. Authorea collaboratively written paper ([link](https://www.authorea.com/191766/WK1b5oyGEjbI9g2LDC4H_A))
2. Join the Slack Channel! [singlecell-batches.slack.com invite link (expires 2017-08-26)](https://join.slack.com/t/singlecell-batches/shared_invite/MjE4Njk4NTMwMTY0LTE1MDExNzU0NDQtNTQyYTVkNTM5NA)

## Meetings

We have a weekly meeting on Mondays 9am PDT / 12pm EDT ([Link to the Google
Hangouts Call]). This is where we discuss batch effect correction algorithms,
how to use them, data access, and analysis results. Hope to see you there!

## Data Access

### Single-cell Human BJ Fibroblasts produced by CSHL Single Cell Analysis students

The data from the CSHL course is hosted in the publicly viewable s3 bucket
`s3://singlecell-batches/fibroblasts/singlecell-cshl/`. You can view the
contents of this bucket using the Amazon Web Services Command Line Interface ([awscli](https://aws.amazon.com/cli/)):

```
$ aws s3 ls --human-readable s3://singlecell-batches/fibroblasts/singlecell-cshl/
```

That command should output:

```
                           PRE HiSeq_CB1CDANXX/
                           PRE allGroups/
2017-08-15 16:27:11  117.5 MiB Group1.matrix.txt
2017-08-15 16:27:11  117.5 MiB Group2.matrix.txt
2017-08-15 16:27:11  581.2 MiB Group3.matrix.txt
2017-08-15 16:27:11  465.2 MiB Group4.matrix.txt
2017-08-15 16:27:11  175.5 MiB Group5.matrix.txt
2017-08-15 16:27:14   94.3 MiB Group8.matrix.txt
```

To copy these files, you can use the `aws s3 cp` command and the `--exclude`
and `--include` flags to use wildcards. This will recursively copy all files
ending in `.txt` to your current directory (about 1.5 GB). Here is an example
of running the command and the output:

```
$ aws s3 cp --recursive --exclude "*" --include "*.txt" s3://singlecell-batches/fibroblasts/singlecell-cshl/ .
download: s3://singlecell-batches/fibroblasts/singlecell-cshl/Group1.matrix.txt to ./Group1.matrix.txt
download: s3://singlecell-batches/fibroblasts/singlecell-cshl/Group2.matrix.txt to ./Group2.matrix.txt
download: s3://singlecell-batches/fibroblasts/singlecell-cshl/allGroups/allGroups.markers.corrSP.pg.txt to allGroups/allGroups.markers.corrSP.pg.txt
download: s3://singlecell-batches/fibroblasts/singlecell-cshl/allGroups/allGroups.markers.corrSP.tsne.txt to allGroups/allGroups.markers.corrSP.tsne.txt
download: s3://singlecell-batches/fibroblasts/singlecell-cshl/allGroups/allGroups.markers.txt to allGroups/allGroups.markers.txt
download: s3://singlecell-batches/fibroblasts/singlecell-cshl/allGroups/allGroups.matrix.hist.txt to allGroups/allGroups.matrix.hist.txt
download: s3://singlecell-batches/fibroblasts/singlecell-cshl/allGroups/allGroups.samples.txt to allGroups/allGroups.samples.txt
download: s3://singlecell-batches/fibroblasts/singlecell-cshl/Group5.matrix.txt to ./Group5.matrix.txt
download: s3://singlecell-batches/fibroblasts/singlecell-cshl/Group8.matrix.txt to ./Group8.matrix.txt
download: s3://singlecell-batches/fibroblasts/singlecell-cshl/Group4.matrix.txt to ./Group4.matrix.txt
download: s3://singlecell-batches/fibroblasts/singlecell-cshl/Group3.matrix.txt to ./Group3.matrix.txt
```



### Publicly available bulk fibroblast sequencing

Thanks to @[yunfangjuan](https://github.com/yunfangjuan), we also have an
[cloud RNA-seq pipeline](https://github.com/chanzuckerberg/cloud-rnaseq) run on
all publicly available bulk human fibroblast datasets. They are located here:

```
$ aws s3 ls --human-readable s3://singlecell-batches/fibroblasts/public-bulk/
```

Currently, the ~6 terrabytes of files are still transfering and the above `aws
s3 ls` command outputs this:

```
                           PRE 200024565/
                           PRE 200026284/
                           PRE 200030567/
```

Eventually, it will output all the files:

```
                           PRE 200024565/
                           PRE 200026284/
                           PRE 200030567/
                           PRE 200038265/
                           PRE 200055169/
                           PRE 200056293/
                           PRE 200057049/
                           PRE 200061656/
                           PRE 200062776/
                           PRE 200063577/
                           PRE 200063734/
                           PRE 200063738/
                           PRE 200068327/
```


IF you want to look at all the files and their subdirectories, use:

```
$ aws s3 ls --human-readable --recursive s3://singlecell-batches/fibroblasts/public-bulk/
```

To copy ALL the files (**not recommended** as this is 5.2 TB - terabytes), do:

```
aws s3 cp --region us-east-2 s3://singlecell-batches/fibroblasts/public-bulk/ . --recursive
```

To only copy the text files (*recommended*), use the `--exclude "*"` flag to remove all files, and then selectively add the `*.txt` files from htseq, the `*.out` files from STAR, and the `*family.soft.gz` files from SRA:

```
aws s3 cp --region us-east-2 s3://singlecell-batches/fibroblasts/public-bulk/ . --recursive --exclude "*" --include "*.txt" --include "*.csv" --include "*.out" --include "*family.soft.gz"
```

## Git tutorials/Introductions

- [GitHub's git tutorial](https://try.github.io/) - Fun, interactive tutorial from GitHub, within the
  browser (no installation required) #interactive #commandline
- [Git Tutorial for Beginners: Command-Line Fundamentals](https://www.youtube.com/watch?v=HVsySz-h9r4)
  \- Highly rated video of someone explaining Git and command line fundamentals
  \#video
- [Software Carpentry Git Tutorial](https://swcarpentry.github.io/git-novice/)
  \- Gentle introduction to `git` using some cute scenarios #interactive #commandline

## Downloading folders (aka "cloning repositories")


1. Create a folder called `singlecell-batches`. I keep all my github
   repositories in a folder called `~/code` so mine is located in
   `~/code/singlecell-batches`, so for me, the commands are:
   ```
   cd ~/code
   mkdir singlecell-batches
   ```
2. To make a copy of the folder, you want to use the command `git clone` to
   copy the "folder and its entire history of changed files" ("repository").
   Let's say you want to download the folder for the Seurat alignment
   algorithm, `combat`. Then you would do:
    ```
    git clone https://github.com/singlecell-batches/combat
    ```
    Which would create a folder called `combat` on your computer.

## Adding an algorithm


To add an algorithm, use the algorithm template created here:
https://github.com/singlecell-batches/cookiecutter-reproducible-science, which
contains instructions for how to use it and upload the folders to GitHub.



## Getting and Giving Help

We are committed to offering a pleasant setup experience for our learners and organizers.
If you find bugs in our instructions,
or would like to suggest improvements,
please [file an issue][issues]
or [mail us][contact].

[importer]: http://import.github.com/new
[issues]: https://github.com/singlecell-batches/getting-started/issues/new
[contact]: olga.botvinnik@czbiohub.org

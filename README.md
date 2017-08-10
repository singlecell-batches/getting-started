# getting-started
How to get started with the single cell batches comparison


[TOC]: # " "

- [Data and document access](#data-and-document-access)
- [Meetings](#meetings)
- [Git tutorials/Introductions](#git-tutorialsintroductions)
- [Downloading folders (aka "cloning repositories")](#downloading-folders-aka-cloning-repositories)
- [Adding an algorithm](#adding-an-algorithm)
- [Getting and Giving Help](#getting-and-giving-help)

## Data and document access


1. Fill out [this form](https://goo.gl/forms/0zVJkkl0GKjtSrCL2) with your name,
   email, and github username. After you fill that out, you should always have
   seamless access to the websites and services below. If it's not the case,
   email Olga (olga.botvinnik-youknowwhatgoeshere-czbiohub.org)
   1. Calendar events ([link](https://calendar.google.com/calendar/embed?src=czbiohub.org_kmsilch9cs92me1at7152fqfpo%40group.calendar.google.com&ctz=America/Los_Angeles))
   2. Google Drive documents ([link](https://drive.google.com/open?id=0B017aFD5c7rIbG02TzNQMmM2Z2c))
   3. Amazon Web Services storage aka "AWS S3"
   4. GitHub `singlecell-batches` organization
      ([link](https://github.com/singlecell-batches))
   5. Open Science Framework "Single-cell RNA-Seq Batch Effect Algorithm
      Comparison" project ([link](https://osf.io/7xm6k/))
   6. Authorea collaboratively written paper ([link](https://www.authorea.com/191766/WK1b5oyGEjbI9g2LDC4H_A))
2. Join the Slack Channel! http://singlecell-batches.slack.com

## Meetings

We have a weekly meeting at 8am PDT / 11am EDT
([time and date annoucement link](https://www.timeanddate.com/worldclock/fixedtime.html?msg=Single+Cell+Batch+Effect+Correction+Weekly+Meeting&iso=20170803T08&p1=224&ah=1)
\- no worries that the event has passed, though the time will change after the
US does daylight savings). This is where we discuss

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
   cd code
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

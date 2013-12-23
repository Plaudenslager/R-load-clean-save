R-load-clean-save
=================

R code to:
 1. load data from an SPSS (.sav) file,
 2. automatically identify potentially redundant / unnecessary columns,
 3. remove any undesired columns,
 4. and save the result as both RMD and CSV files.


## Expected use case: ##

I often run research projects where I work with a research vendor to design, field, and analyze the results of a survey.  Typically, along with their analysis in PowerPoint, I can request the SPSS file containing the raw responses.  Sometimes, those raw responses are not well cleaned of survey management cruft, so they contain lots of columns that don't correspond to any of the original survey questions, and some of these columns just repeat the same value. (I can only assume that they vary across surveys).

To do my own analysis in R or Excel, I need to convert these files into those formats.  Further, I like to clean out any columns that arent useful.  Since these surveys often return hundreds of columns, it is helpful to automatically detect any that look like they don't contain any useful data.  I may also notice some columns that contain uninteligible, and therefore unusable data (e.g. some internal code related to a research subcontractor).

## Runtime environment ##

The code is written in RMD, which is R Markdown.  Most of the file is text-based instructions and commentary written in Markdown, with sections of R code.  R-Studio (www.rstudio.com) can open and recognize this type of file, and using a process called "Knit", it will produce an HTML output document that includes the comments, the code blocks, and the results of the code.  This provides a nice piece of documentation on how you got from the raw data file to the finished files, and is consumable by nearly everyone, with no special software.  This helps remind you of what transformations / additions / deletions you did (or the software did for you), and lets others check your work.

If you don't have easy access to R-Studio, you can just use the code in the code blocks.  Code blocks start with:
``` {r}

and end with 

```

Just copy the code blocks (without the tic-marks) to a text file, and run it as R code.

## Instructions: ##

Everything above the comment "Set project parameters" is just instructions.  Immediatelyl following that comment, you will want to set your _working directory_, your _raw file name_ (i.e. the SPSS file name), and your _clean file name_, which will be used with _.R_ and _.csv_ extensions.  These two files can be used for analysis in R and Excel (or nearly any other tool), respectively.

If you do nothing but set the parameters above, you will get a complete conversion of the entire raw data file into the two output formats.  You will also get a couple of listings in your HTML document (or on the screen if you are just running the R commands).  First will be a list of all the column names, so you know what is in the raw data file.  Hopefully these are descriptive, or you already know how to decode them.  You will also get a listing of columns that are filled with a repeating value; these columns can probably be deleted. These columns names are also stored in a variable called _cut list_. Finally, you will see a list of the cleaned column names, which will be written to the two output files.  At this point, the list of raw columns and cleaned columns will be the same

__Although the program can detect 'junk' columns, by default, it will not automatically remove them.__

To delete columns, find the heading __Clear out unnecessary columns (manually)__.  Find the variable _remove_, and add column numbers between the parentheses.  I typically view the list of 'junk' columns, and then add them manually to the _remove_ list.  You could just assign the _cut list_ variable to _remove_, but since I almost always want to remove additional columns, I like to have an explicit list.

The remainder of the program will just display the column names of the cleaned data, and save them to the working directory, using the same name for both files (defined in variables near the top).

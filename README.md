# MyM2R - a David L. Bijl creation

At PBL Netherlands Environmental Assessment Agency we apply the MyM programming language for some of our modelling work. The inputs to these models need a particular formatting in order to process the data without (fatal) errors. To circumvent the use of our Excel macro's reformatting excel sheets, and to enter the new era of data processing, one of our former team members (David Bijl) had programmed a couple of functions to make life for all superstaR's more easy. To make MyM2R more easily available, I have put it up for easy download on github.


# installing MyM2R
To install MyM2R from github, use the following line of code:

Requires the devtools package:
```
install.packages("devtools")
library("devtools")
```

Code to install MyM2R:
```
install_github("marieyesse/mym2r")
```

# Using the MyM2R package

## Reading MyM files to R.
Reading MyM file to R:

```
# assumes you know the exact structure of the MyM file you are going to read
# Define parameters, e.g.
mym.folder = "input/water model/mym output/"  
regions28 = c(1:26,"dummy","TOTAL")
cooling5   = c("dry","once","sea","pond","tower")
minmedmax  = c('max','med','min')  

read.mym2r.nice(mym.folder=mym.folder, 
                scen.econ='SSP2', 
                filename='ElecWWD_3_Int', 
                collist=list(regions28,1:29,cooling5,minmedmax), 
                namecols=c('region','tech','cool','est')) 
  
```


Reading and collating multiple MyM files into R

```
# purpose: read many MyM files at once
# path.to.folder is the full path to the folder where the .out files are. A slash is added if omitted.
# note:   extension '.out' is added if omitted

read.mym2r.many(filenames=c(), 
                path.to.folder='')
                
```

## Writing R data to MyM files
Here is an example that can be used seperately or in looping. Editable elements are addressed:

```
# Define your parameters
RELEVANT_INFO = 'The source of my data is NAME (YEAR) http://www.example_here.blah'

  write.r2mym(data = YOUR_DF_IN_R, 
              outputfile = 'FOLDER_STRUCTURE/FILE.out', 
              value.var = 'COLUMN_WITH_VALUES', 
              MyM.vartype = 'REAL',
              MyM.varname = 'main.CHECK_ORIGINAL_FILE', 
              comment.line = RELEVANT_INFO,
              time.dependent = TRUE)
```

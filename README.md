# Class Assignment BICB 5309

## Goals:

We are going to explore metagenomes using a database curated by MGinfy for a metabolic network [DETERMINE LATER]. 



## Background Information on Metabolic network

Background information DOI: 10.1073/pnas.2312652121

[Add more later.]

## Explore Jupyter Notebook

Cal will present on screen the basics of jupyter notebook.  [Open your jupyter notebook here.](notebooks.msi.umn.edu)
We are going to be using Jupyter notebooks.  *This interactive computing environment requires only a web browser, and enables data analysis and visualization on our HPC resources in a shareable, reproducible notebook format.*  

This means that we are going to be working in a non local computing environment, and we will need to transfer our output files to our local computers.  We will use WINSCP.  By next class period, download and [configure WinSCP](https://www.msi.umn.edu/support/faq/how-do-i-use-winscp-transfer-data)  for Windows users and [FileZilla](https://www.msi.umn.edu/support/faq/how-do-i-use-filezilla-transfer-data) for Mac users.

## Setting up

The databases, R packages, and scripts are all already installed on this MSI environment. You will just need to copy a few of these files and set up a directory.

```bash
# This is a comment line.  Comment lines begin with a "#". It shouldn't be a problem if they are in your code, because bash (the language we are coding in) ignores them.

# Create a conda environment to run blast searches and to synergize with our R packages
# Create conda environment from the file in the public directory.
module load conda 
conda env create -f ~/../public/mgmap.yml
conda deactivate
conda activate mgmap

# If those last two lines do not work.  Restart your Jupyter Notebook by starting and stopping your server through the Hub Control Pannel under 'File'.
```

Create some directories that our R file will recognize. Run the following code in your terminal.

```bash
#mkdir makes a directory/folder
mkdir mgmap
# cd changes your current directory
cd mgmap
# ls lists all files and diretories in your current directory
ls
mkdir input
mkdir output
```

Now we have all of the required directories. We are going to copy a few of the scripts. You will edit these scripts, so copy and don't move them!

```bash
cp ~/../public/Mgnify_search_fv.R
cp ~/../public/run_Mgnify_search_map.txt
```

## Section for FASTA FILES AND BLAST

```bash
cd ~/mgmap # move to mgmap folder
nano fasta.fasta # create a fasta file to blast search
blastp -query fasta.fasta -db ww_proteins.faa -outfmt 6 -max_target_seqs num_sequences > /input/fasta_ww_blast.out
# enter the max number of sequences you wish to retrieve: num_sequences
# enter the fasta file: fasta.file
# change the name of your output file: fasta_ww_blast.out
cd ..
```

## Run the mgmap sequence

Create a [geonames](http://www.geonames.org/) account and add it to the user parameters!
After confirming your account you need to allow access to the [geonames webservices](http://www.geonames.org/enablefreewebservice).

Open the Mgnify_search_fv.R file and change the following variables to match your search.

1. geonamesUsername
2. pid_cutoff
3. blast_search
4. prot_names
5. thresh (optional)

You will also need to add your email to the run_Mgnify_search_map.txt script.

This script is formatted as a slurm script.  Slurm is a type of script that requests resources from a larger computer and runs a script independent of your terminal.


```bash
sbatch -p small run_Mgnify_search_map.txt
```

## Assignment questions

***To potentially be changed before the class period***

### 1. Where are waste water genes over time? (2pts)

Look at the metadata file in the output. Where are genes located over time?  What does that say about Metformin?  What trend would you expect with something like galgene and why? ***Connect this question better to the paper***

### 2. Using the mgmap script and metagenomic data(2pts)

What can we conclude about metagenomic data?  Are the genes found on the map in the same organism?  If you found a crcB gene (a fluoride exporter) in a sample and a defluorinase gene at the same site, would the site be capable of defluorination?  Why or why not?

### 3. NEED TO ADD MORE QUESTIONS!!!



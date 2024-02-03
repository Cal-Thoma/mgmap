# mgmap
## Important files

1. "proteins_ww_clusterreps_fullen.csv": Comma Seperated Value file containing cluster metadata for all waste water clusters
2. "ww_proteins.faa": fasta file containing all waste water proteins
3. "mgmap.yml": yml file that will be used to create the conda environment.
4. Hidden folder with all R packages necessary.
5. "Mgnify_search_fv.R": The main function!!

## Setting up

Download the required files and unzip them.  This downloads from my google drive file.

```bash

tar -xvzf mgmap.tar.gz
```

Move to the folder mgmap, first.


```bash
# Using the first time
conda env create -f mgmap.yml
### All subsequent uses you will need to load the conda environment.
# Deactivate your current conda environment
conda deactivate
conda activate mgmap
```

You will be able to run blast searches from this environment!

### Make blastdb using linux commands.

```bash
cd blast_ww
makeblastdb -in ww_proteins.faa -dbtype prot
cd ..
```

### Blast a sequence

```bash
cd blast_ww # move to blast folder
nano fasta.fasta # create a fasta file to blast search
blastp -query fasta.fasta -db ww_proteins.faa -outfmt 6 -max_target_seqs num_sequences > ../input/carC_ww_blast.out # enter the max number of sequences you wish to retrieve.
cd ..
```

## Run the mgmap sequence

Finally run the mgmap! (change your parameters to match your input file and other specifications).
Create a [geonames](http://www.geonames.org/) account and add it to the user parameters!

```bash
Rscript Mgnify_search_fv.R
```

This will have a lot of random warnings.  They can all be ignored, unless you do not see output. Most things that go wrong are error handled and will appear in an error file in the output folder with instructions on fixing them.

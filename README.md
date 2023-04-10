# Download-fastq-files-using-SRA-Toolkit

Install sra toolkit:

Download sra toolkit:
  wget --output-document sratoolkit.tar.gz https://ftp-trace.ncbi.nlm.nih.gov/sra/sdk/current/sratoolkit.current-ubuntu64.tar.gz

Extract the contents 
  tar -vxzf sratoolkit.tar.gz

Go to where the binaries are
  cd sratoolkit.tar.gz/bin
  pwd

Append the path to the binaries to your PATH environment variable:
  <export PATH=$PATH:$PWD/sratoolkit.3.0.0-mac64/bin>
  
Verify that the binaries will be found by the shell:
  which fastq-dump
This should produce output similar to:/Users/JoeUser/sratoolkit.3.0.0-mac64/bin/fastq-dump

Download single file:
  prefetch SRR11309784
  fasterq-dump SRR11309784 --split-files --skip-technical 
  
  where --split-files will generate SRR.1_fastq and SRR_2.fastq files
  
Download multiple files (with SRR numbers in a text file) 
- you can grab a BioProject/SRP accession list (Send to - File - Accession List) and save it to default SRA tools /sra directory
- or you can create a file called `srr_id.txt` with files you want to download; you need to get the SRR numbers from the BioProject (same as before)
- Use the `prefetch` command to download the SRA files for the SRR numbers listed in your file.
  prefetch --option-file srr_id.txt
- Use the `fasterq-dump` command to convert the SRA files to FASTQ format
  cat srr_id.txt | xargs fasterq-dump --outdir "/your-directory/for-fastq"

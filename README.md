# seqCompare
A toolkit for nucleotide sequence similarity analysis

# Installation

```
conda env create --name seqCompare --file environment.yaml --yes
pip install seqCompare
```

Upcoming...

```
conda install -c bioconda seqCompare --yes
```

# Calculate percent similarity of sequences
```
seqCompare similarity --help

options:
  -h, --help            show this help message and exit
  --data, -d data       input text file (list of fasta files, alignment, or presence/absence table)
  --format, -f format   data format (default: tsv)
  --output, -o output   output percent similarity
  --length, -l length   k-mer length for --mash/-m or --fastani/-n (default: 31)
  --size, -s size       sketch size for MASH; use with --mash (default: 1000000)
  --mash, -m            calculate similarity using MASH
  --fastani, -n         calculate similarity using fastANI
  --blast, -b           calculate similarity using BLAST
  --matrix, -x          calculate similarity using a presence and absence matrix
  --blastani, -i        calculate blast ANI similarity
  --aln, -a             calculate similarity based on a given sequence alignment
  --fraction, -c fraction
                        minimum overlap fraction with shorter sequence for ANI calculation; use with --fastani or --blastani (default: 0.70)
  --fragment, -r fragment
                        fragment length for calculating ANI; use with --fastani (default: 500)
  --evalue, -e evalue   minimum evalue for hits; use with --blast (default: 0.001)
  --qcovperhsp, -p queryCovPercentHSP
                        minimum query coverage for each blast hsp (default: 10)
  --threads, -t threads
                        number of threads (default: 5)
```

```
seqCompare similarity --blast --data input.txt --output out.similarity.blast.tsv --threads 20 --length 28 
```

```
seqCompare similarity --blastani --data input.txt --output out.similarity.blastani.tsv --threads 20 --length 28 
```

```
seqCompare similarity --fastani --data input.txt --output out.similarity.fastani.tsv --threads 20 --length 15 
```

```
seqCompare similarity --matrix --data input.table.txt --output out.similarity.matrix.tsv --threads 20 --length 15 
```

# Query or screen sequences against reference sequences

```
seqCompare query --help

options:
  -h, --help            show this help message and exit
  --reference, -r reference
                        input tabular text file containing reference sequences
  --query, -q query     input tabular text file containing query sequences
  --format, -f format   data format (default: tsv)
  --output, -o output   output percent similarity
  --length, -l length   k-mer length for --mash/-m or --fastani/-n (default: 31)
  --evalue, -e evalue   minimum evalue for hits; use with --blast (default: 0.001)
  --qcovperhsp, -p queryCovPercentHSP
                        minimum query coverage for each blast hsp (default: 10)
  --complete, -c        comparing full sequences
  --threads, -t threads
                        number of threads (default: 5)
```

```
seqCompare query --reference references.txt --query input.txt --output out.matching.blast.tsv --length 28 --threads 20
````

# Cluster sequences based on sequence similarity values

```
seqCompare cluster --help

options:
  -h, --help            show this help message and exit
  --data, -d data       input tabular text file
  --format, -f format   data format (default: tsv)
  --output, -o output   output clusters
  --prefix, -p prefix   cluster label prefix
  --sep, -s separator   lineage label separator
  --thresholds, -t [thresholds ...]
                        cluster or lineage thresholds
```

```
seqCompare cluster -d out.similarity.blast.tsv -t 50 85 -o out.similarity.50.85.tsv
```

# Order presence and absence data file

```
seqCompare order --help

options:
  -h, --help            show this help message and exit
  --data, -d data       input tabular text file
  --format, -f format   data format (default: tsv)
  --output, -o output   output ordered data file
  --rownames, -r rownames
                        order by item names in a given text file (one name per row)
  --threads, -t threads
                        number of threads (default: 5)
```

# Rename rows and columns in a presence and absence file

```
seqCompare rename --help

options:
  -h, --help            show this help message and exit
  --data, -d data       input tabular text file
  --format, -f format   data format (default: tsv)
  --output, -o output   output ordered data file
  --columns, -c [columns ...]
                        selected column numbers (e.g., --columns 1 2 3 4)
  --newdata, -n newdata
                        order by item names in a given text file (one name per row)
```

# Filter rows and columns in a presence and absence file

```
seqCompare filter --help

options:
  -h, --help            show this help message and exit
  --data, -d data       input tabular text file
  --format, -f format   data format (default: tsv)
  --output, -o output   output percent similarity
  --min, -a minCutoff   select with frequency ≥minCutoff percent (overrides --columns/-c and --rows/-r)
  --max, -b maxCutoff   select with frequency ≤maxCutoff percent (overrides --columns/-c and --rows/-r)
  --columns, -c columns
                        select only columns present in a given text file (one column value per row)
  --rows, -r rows       select only rows present in a given text file (one column value per row)
  --threads, -t threads
                        number of threads (default: 5)
```

# Sample rows and columns in a presence and absence file

```
seqCompare sample --help

options:
  -h, --help           show this help message and exit
  --data, -d data      input tabular text file
  --format, -f format  data format (default: tsv)
  --output, -o output  output file
  --cf, -c colfreq     randomly select ≥colfreq percent of the columns
  --rf, -r rowfreq     randomly select ≥rowfreq percent of the rows
```

# Transpose rows and columns in a presence and absence file

```
seqCompare transpose --help

options:
  -h, --help           show this help message and exit
  --data, -d data      input tabular text file
  --format, -f format  data format (default: tsv)
  --output, -o output  output percent similarity
```

# Create a k-mer presence and absence table or matrix given a list of sequences

```
seqCompare table --help

options:
  -h, --help            show this help message and exit
  --data, -d data       input text files containing fasta sequence file names
  --output, -o output   output percent similarity
  --length, -l length   k-mer length (default: 31)
  --min, -m minabundance
                        minimum k-mer abundance (default: 1)
  --maxmem, -x maxmemory
                        maximum memory (default: 5000)
  --dsk, -s             DSK to identify k-mers
  --bifrost, -b         bifrost to identify variable length k-mers or unitigs
  --kmers, -k kmers     only query input sequence against a given k-mer database
  --approx, -a          search inexact k-mers (default: False)
  --threads, -t threads
                        number of threads (default: 5)
```

# Show software version

```
seqCompare version --help

options:
  -h, --help     show this help message and exit
  --version, -v  show software version
```

# Show citation information

```
seqCompare citation --help

options:
  -h, --help      show this help message and exit
  --citation, -c  show software citation information
```

# Citation
```
Chaguza et al. seqCompare: A toolkit for nucleotide sequence similarity analysis. 2026. [https://github.com/ChrispinChaguza/seqCompare](https://github.com/ChrispinChaguza/seqCompare)
```

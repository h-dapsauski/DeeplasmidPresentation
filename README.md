# Deeplasmid

Deeplasmid is a machine learning tool used to distinguish plasmids from bacterial chromosomes based on the DNA sequence and its encoded biological data. The input sequences are in the form of contigs, stored in a .fasta file. 



## Deeplasmid Docker image for CPU-only on Ubuntu 20.04.3 with Ryzen processor
Input: .fasta file 

Output: Directory of results 

To run the Deeplasmid Docker container, you first need to install the docker on your system. Then make an account and register on dockerhub. Then pull the deeplasmid image from dockerhub using the following: 

```
docker login
docker pull billandreo/deeplasmid-cpu-ubuntu2
```

Running Deeplasmid 

```
docker run -it -v /path/to/input/fasta:/srv/jgi-ml/classifier/dl/in.fasta -v /path/to/output/directory:/srv/jgi-ml/classifier/dl/outdir billandreo/deeplasmid-cpu-ubuntu2 deeplasmid.sh in.fasta outdir
```

## Citation

William B Andreopoulos, Alexander M Geller, Miriam Lucke, Jan Balewski, Alicia Clum, Natalia N Ivanova, Asaf Levy, Deeplasmid: deep learning accurately separates plasmids from bacterial chromosomes, Nucleic Acids Research, 2021;, gkab1115, https://doi.org/10.1093/nar/gkab1115

https://github.com/wandreopoulos/deeplasmid




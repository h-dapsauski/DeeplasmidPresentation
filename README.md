# Deeplasmid

Deeplasmid is a machine learning tool used to distinguish plasmids from bacterial chromosomes based on the DNA sequence and its encoded biological data. The input sequences are in the form of contigs, stored in a .fasta file. 


## Deeplasmid Docker image for CPU-only on Ubuntu 20.04.3 with Ryzen processor
Input: .fasta file 

Output: Directory of results 

The output file predictions.txt contains plasmid predictions for each contig in the input file. Each contig is given a 'score'; a value closer to 1.0 indicates a high probability of being a plasmid. This score will be listed after the contig/node name. 

- Longer than 330k bases (possibly a chromosome or megaplasmid)
- Shorter than 1k bases (inconclusive)
- Plasmid with score near 1.0
- Ambiguous have scores around 0.5 (gray zone)
- Chromosome (non-plasmid) with score near 0.0

## Explanation of Docker 

Docker is a platform that allows you to package and run applications in isolated environments called containers. Containers bundle all the necessary software and dependencies needed for the application, so it runs the same way regardless of the system it's on. This means users can run Deeplasmid with all of the necessary dependencies without needing to manually install them. To run the container, pull the Docker image and run it. Docker containers are lightweight, efficient, and ideal for deploying applications consistently across different environments.

### Running the Container 

To run the Deeplasmid Docker container, you first need to install the docker on your system. Then make an account and register on dockerhub. Then pull the deeplasmid image from dockerhub using the following: 

```
docker login
docker pull billandreo/deeplasmid-cpu-ubuntu2
```

Run Deeplasmid for plasmid identification using the following command:
```
docker run -it -v /path/to/input/fasta:/srv/jgi-ml/classifier/dl/in.fasta -v /path/to/output/directory:/srv/jgi-ml/classifier/dl/outdir billandreo/deeplasmid-cpu-ubuntu2 deeplasmid.sh in.fasta outdir
```
* Make sure to change the input file path (/path/to/input/fasta) and the output directory path (/path/to/output/directory) with full file paths to the corresponding input file and output directory 
* Depending on user permissions, the docker pull command may need to be run with sudo 

### Alternative Docker Image with GPU support 

```
docker login
docker pull billandreo/deeplasmid.tf.gpu3
```

Run Deeplasmid for plasmid identification with GPU using the command below:

```
~/Downloads/deeplasmid/classifier/dl$ sudo /usr/bin/docker run -it  --gpus all   -v `pwd`/testing/649989979/649989979.fna:/srv/jgi-ml/classifier/dl/in.fasta  -v  `pwd`/testing/649989979/649989979.fna.OUT:/srv/jgi-ml/classifier/dl/outdir   billandreo/deeplasmid.tf.gpu3   deeplasmid.sh  in.fasta outdir
```

### Building Docker Image for GPU 

```
    sudo docker rm $(sudo docker ps --filter status=exited -q)
    sudo docker images
    sudo docker rmi ...ids....
    sudo docker build -t billandreo/deeplasmid.tf.gpu3 -f Dockerfile.GPU3 .
```


## Citations

William B Andreopoulos, Alexander M Geller, Miriam Lucke, Jan Balewski, Alicia Clum, Natalia N Ivanova, Asaf Levy, Deeplasmid: deep learning accurately separates plasmids from bacterial chromosomes, Nucleic Acids Research, 2021;, gkab1115, https://doi.org/10.1093/nar/gkab1115

https://github.com/wandreopoulos/deeplasmid




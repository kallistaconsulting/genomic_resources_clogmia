# Genome Resources: Clogmia Start-Up

This project contains two components:

1. A Docker container  
2. A setup script for a pre-configured Drupal website to make finding and using tools easier.

---

## 1) Container (Required)

The container provides a self-contained set of tools preinstalled and pre-configured with the genome data for *Clogmia albipunctata* (other versions upcoming):

- **JBrowse 2** (genome browser)  
- **SequenceServer 2.0** (web-based BLAST server with links back to JBrowse)  
- **Shiny Server** (for R/Shiny applications that link back to JBrowse and BLAST)  
- **Dependencies** (Samtools, BLAST+, Tabix, R, Bioconductor, etc.)

All tools are integrated with genomic data pulled from a GitHub release tarball.

### Installing the Container

```bash
# Clone the repository
git clone https://github.com/kallistaconsulting/genomic_resources_clogmia.git
cd genomic_resources_clogmia

# Build and run the container
sudo bash setup.sh
```

This runs a docker build command (docker build -t genome_browser .) and a docker run command.  The docker run command creates an environmental variable in the docker that contains the host IP (necessary for SequenceServer2.0 link backs to JBrowse) and links ports from the container to the host machine.

Note: this will take about 30m to install, mainly due to installation of R packages.  Testing indicated 40Gb root directory was sufficient, 20Gb was not.

From here, you can run any of the tools from a web browser with the proper links:
* IP:3000?config=clogmia.json  → JBrowse2 instance
* IP:3838/freeCount/apps/DA/ → edgeR differential expression applications
* IP:3838/freeCount/apps/FA/ → topGO and GSEA functional enrichment applications
* IP:3838/crisprFinder → views pre-profiled transcriptome to aid in initial design of sgRNA
* IP:3838/crisprViewer → views pre-created crispr sgRNA primer design tables
* IP:4567 → SequenceServer2.0 instance with blast databases and JBrowse2 link backs

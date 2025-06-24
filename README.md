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

### 2) Webpage set up (optional but recommended)
Tools are integrated into a pre-configured Drupal website that has links to all the above, plus locations for Downloads (upcoming), publications, etc.  An example is currently available at: http://149.165.151.125/home

### Installing the website
1. On the local machine:

```bash
cd /var/www/genomic_resources_clogmia/drupal
```

2. Edit init.sql
This file defines your username, database name, and password.  You will want to edit this from the defaults to provide security, as the defaults are used and they are publicly known.  Change ‘drupalpass’ to any password you would like to use.

3. Run install script:
``` bash
sudo bash setup.sh
```

This script will setup Drupal in the local machine’s /var/www/html directory.  Drupal 9.5.11 will be installed, the business theme used for the site will be pulled, and the mysql database that hold the site information will be imported.
You will need to input the password you set in step 2.  

You should now be able to access the website from your own IP/home (e.g. 149.165.151.125/home).  All tools are linked with dynamic links, meaning the host IP does not matter.  

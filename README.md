# genomic_resources_clogmia
resources for the docker version of the browser ecosystem

## Installation - tools
clone down the repo into home dir of fresh VM (tested on Jetstream)

run: sudo bash setup.sh

this will take ~30m to install jbrowse, blast, rnaseq and crispr tools, and populate them

you can stop here, or build the webpage to make organization easier

## Installation - webpage

cd drupal

run: sudo bash setup.sh

answer questions as they come, set password (I use "clogmia")

when asked for password, use this one.

go to IP of VM -> drupal page is populated :)

Bacterial genome assembly pipeline
=======================

This pipeline assembles Illumina paired end reads. It results in a scaffold and annotated assembly.

#Requirements:

-Linux 64 bit system<br />

-python (version 2.7)<br />
-SPAdes (version 3.10.1)<br />
-samtools (version 1.3)<br />
-prokka (version 1.12)<br />
-bowtie2 (version 2.3.0)<br />

#Installation:


#Usage:

  sh bacteria_assembly.sh <Sample_ID> <Reads_R1> <Reads_R2> <Genus> <species> <Number_of_cores>
 
  <Sample_ID>               Unique identifier for the sample
  <Reads_R1>                Foreward read file
  <Reads_R2>                Reversed read file
  <Genus>                   Genus name of the bacterial species
  <species>                 Species name of the bacterial species
  <Number_of_cores>         number of parallel threads to run (int)

#example:

"
#!/bin/sh
#$ -q all.q
#$ -e $JOB_ID.cov.err
#$ -o $JOB_ID.cov.out
#$ -cwd
#$ -pe smp 24

module add UHTS/Assembler/SPAdes/3.10.1;
module add UHTS/Analysis/samtools/1.3;
module add UHTS/Analysis/prokka/1.12;
module add UHTS/Aligner/bowtie2/2.3.0;

for i in FAM22234

do

sh /home/dwuethrich/Application/assembly_pipeline/bacteria_assembly.sh "$i" ../../reads/"$i"_R1.fastq.gz ../../reads/"$i"_R2.fastq.gz Pediococcus acidilactici "$NSLOTS"

done
"
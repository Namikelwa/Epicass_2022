Downloading files
scp student11@IP:~/data/duplicate /path/to/computer 
#scp-securecopy from(path) to(path) 


Genome Assembly
## Data 
Escherichia coli was sequenced using the MiSeq platform (2 x 250bp). The reads were deposited in the NCBI SRA database under the accession SRR12793243.

You need SRA toolkit installed before going ahead to download data

fastq-dump -I SRR12793243  --split-files

The above command will download two files: SRR12793243_1.fastq.gz and SRR12793243_2.fastq.gz.

data directory 
/home/Epicass_workshop/Day3/Data/illumina/

## Data Quality Check
The downloaded fastq files are raw data, therefore we have to do some quality checks and quality trimming of the data.
we create indir and XX variables assigning the PATH and the accession number to it. By doing this, we can provide the input files in a short and easy way

indir="/home/Epicass_workshop/Day3/Data/illumina/"

XX="SRR12793243"
Now we need to run the FastQC program to see the quality of raw data.You may store the output in /home/Epicass_workshop/Day3/myResults directory.
We must create the outdir variable and then create the directories.

outdir="/home/Epicass_workshop/Day3/myResults"
mkdir ${outdir}
mkdir ${outdir}/fastqc
mkdir ${outdir}/fastp

fastqc -t 4 ${indir}/${XX}_*.fastq.gz -o ${outdir}/fastqc 

check the results of the above command by downloading the *.html file to your local computer and looking at it with your browser

Trimmimg/Filtering

fastp -i ${indir}/${XX}_1.fastq.gz -I ${indir}/${XX}_2.fastq.gz 
-o ${outdir}/fastp/${XX}_1trim.fastq.gz -O ${outdir}/fastp/${XX}_2trim.fastq.gz 
-j ${outdir}/fastp/${XX}_fastp.json  -h  ${outdir}/fastp/ 
${XX}_fastp.html --thread 4 --trim_poly_g -l 250 -q 20 -n 0

The quality-filtered files are stored as SRR12793243_1trim.fastq.gz and SRR12793243_2trim.fastq.gz in the fastp folder under results directory.
Run the FastQC again on the quality trimmed data and you will see quality metrics of the trimmed data.

fastqc -t 4 ${outdir}/fastp/${XX}_*trim.fastq.gz -o ${outdir}/fastqc

You can check the output by downloading the *.html files in your local computer and open them with your browser

## Genome Assembly
de novo assembly with Illumina short paired-end reads
We are using Spades 
spades.py --careful -m 16 -t 8 -k 21,33,55,77,99,127 -1 ${outdir}/fastp/${XX}_1trim.fastq.gz -2 ${outdir}/fastp/${XX}_2trim.fastq.gz -o ${outdir}/asm_spades
The result of the assembly is in the path /Epicass_workshop/day3/results/asm_spades containing scaffolds.fasta and  assembly_graph_with_scaffolds.gfa files.



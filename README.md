# Command_line_tricks

daily documenting the problems i solve on the command line


# add kernel to your virtual environment

python -m ipykernel install --user name=kernel_name

# samtools view

help convert SAM file to BAM file 
-h returns header


samtools view -F 4 -h file.sam -o file.bam


if you don't use -h, it truncates the file and you cannot perform samtools sort

# use GNU parallel to speed up jobs
ls *.sorted.bam | parallel "bedtools intersect -v -a {} -b input.bed > {.).new.bam

{} means the list from ls
{.} will replace the suffix .sorted.bam with .new.bam

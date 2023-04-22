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

# R trick Subset 23 chr from dataframe

subset(esc.bed, grepl("^chr[0-9]{1,2}$|^chr[XY]$", seqnames))

# seperate columns by tab

awk {'print $1"\t"$2"\t"$3'} data.txt

# great resource for learning command line manipulations

https://learnbyexample.gitbooks.io/command-line-text-processing/content/gnu_awk.html

# use the mv command to rename file

mv "$file" "${file/annotated_peaks/annotated_peaks}"

# create 3 column bed file with awk

for file in annotated_peaks*; do
  tail -n +2 $file | cut -f1-3 -d$'\t' > "${file}_columns.txt"
done

# remove last 4 lines with awk

sed -i -n -e :a -e '1,4!{P;N;D;};N;ba' file.txt

# remove the first lines of multiple bed files while concatenating them and printing 2,3,4 column

tail -n 2 file.bed file2.bed file3.bed > out.bed
awk '{print $2"\t"$3"\t"$4}'

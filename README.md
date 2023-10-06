# hse23_hw1
**1. Создание ссылок в папке**  
ls /usr/share/data-minor-bioinf/assembly/* | xargs -tI{} ln -s {}  
**2. Выбор случайныйх чтений**    
SEED=727  
seqtk sample -s$SEED oil_R1.fastq 5000000 > R1_PE.fastq  
seqtk sample -s$SEED oil_R2.fastq 5000000 > R1_PE.fastq  
seqtk sample -s$SEED oilMP_S4_L001_R1_001.fastq 1500000 > R1_MP.fastq   
seqtk sample -s$SEED oilMP_S4_L001_R2_001.fastq 1500000 > R1_MP.fastq  
**3. Оценка чтений используя FastQC**    
mkdir fastqc  
ls sub* matep* | xargs -tI{} fastqc -o fastqc {}  
**4. Создание отчета через MultiQC**  
mkdir multiqc  
multiqc -o multiqc fastqc  
**5. Обрезание чтений**  
platanus_trim sub*  
platanus_internal_trim matep*  
**6. Удаление изначальных файлов**  
rm *.fastq  
**7. Оценка качества обрезанных чтений используя FastQC**
mkdir fastqc_trimmed  
ls sub* matep*| xargs -tI{} fastqc -o fastqc_trimmed {}  
**8. Создание отчета для обрезанных чтений через MultiQC**  
mkdir multiqc_trimmed  
multiqc -o multiqc_trimmed fastqc_trimmed  
**9. Сбор контиг**  
time platanus assemble -o Poil -f trimmed_fastq/R1_PE.fastq.trimmed trimmed_fastq/R2_PE.fastq.trimmed 2> assemble.log &  
**10. Сбор скаффолдов**  
1) time platanus scaffold -o Poil -c Poil_contig.fa -IP1 trimmed_fastq/R1_PE.fastq.trimmed trimmed_fastq/R2_PE.fastq.trimmed -OP2 trimmed_fastq/R1_MP.fastq.int_trimmed trimmed_fastq/R2_MP.fastq.int_trimmed 2> scaffold.log &  
2) echo scaffold1_len3834389_cov231 > scaffold_name.txt  
3) seqtk subseq Poil_scaffold.fa scaffold_name.txt > longest_scaffold.fna
**11. Gap_close**
1) time platanus gap_close -o Poil -c Poil_scaffold.fa -IP1 trimmed_fastq/R1_PE.fastq.trimmed  trimmed_fastq/R2_PE.fastq.trimmed -OP2 trimmed_fastq/R1_MP.fastq.int_trimmed trimmed_fastq/R2_MP.fastq.int_trimmed 2> gapclose.log &  
2) echo scaffold1_cov231 > longest_scaffold_gapclosed.txt  
3) seqtk subseq Poil_gapClosed.fa longest_scaffold_gapclosed.txt > longest_scaffold_gapclosed.fna
**12. Не trimmed**
![image1](https://github.com/admukhortikova/hse23_hw1/assets/146677685/a14de087-1e85-4982-9e97-927abea25165)  
![image2](https://github.com/admukhortikova/hse23_hw1/assets/146677685/b121ab7d-fef0-44ee-ae26-bc6e1486d069)
![image3](https://github.com/admukhortikova/hse23_hw1/assets/146677685/3bf1c9d6-64ee-4143-a8b9-31bdff71dd07)
![image4](https://github.com/admukhortikova/hse23_hw1/assets/146677685/9dc1fe62-ae50-4bc8-b3aa-5dc1900fedb9)
![image5](https://github.com/admukhortikova/hse23_hw1/assets/146677685/09ff1666-b04c-4a96-bb78-d7135e77b78b)  

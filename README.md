# hse23_hw1
**1. Создание ссылок в папке**  
ls /usr/share/data-minor-bioinf/assembly/* | xargs -tI{} ln -s {}  
**2. Выбор случайныйх чтений**    
SEED=727  
seqtk sample -s$SEED oil_R1.fastq 5000000 > sub1.fastq  
seqtk sample -s$SEED oil_R2.fastq 5000000 > sub2.fastq  
seqtk sample -s$SEED oilMP_S4_L001_R1_001.fastq 1500000 > matep1.fastq  
seqtk sample -s$SEED oilMP_S4_L001_R2_001.fastq 1500000 > matep2.fastq  
**3. Оценка чтений используя FastQC**    
mkdir fastqc  
ls sub* matep* | xargs -tI{} fastqc -o fastqc {}  

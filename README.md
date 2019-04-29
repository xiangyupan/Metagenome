Pipeline of analysing metagenomic data-beta
-----------------------------------------   
General pipeline to obtain the gene abundence matrix and to annotate taxaonomic/function database   
###Binning pipeline      
`ln -s /lustre/sdb/lingen/workB/01.meta/03.Assembly/Hay_Cecum-1.contigs`   
`/lustre/sdb/taoye/mybin/Module_Meta/bwa index Hay_Cecum-1.contigs`     
`/lustre/sdb/taoye/mybin/Module_Meta/samtools faidx Hay_Cecum-1.contigs`      
`/lustre/sdb/taoye/mybin/Module_Meta/bwa mem -t 40 -M -R '@RG\tID:Hay_Cecum-1\tSM:Hay_Cecum-1\tLB:Hay_Cecum-1\tPL:Illumina\tPI:500' Hay_Cecum-1.contigs /lustre/sdb/lingen/workB/01.meta/01.QC/Hay_Cecum-1.clip.1.fq.gz /lustre/sdb/lingen/workB/01.meta/01.QC/Hay_Cecum-1.clip.2.fq.gz | /lustre/sdb/taoye/mybin/Module_Meta/samtools view -bS -t Hay_Cecum-1.contigs.fai - > Hay_Cecum-1.bam` 
`/lustre/sdb/taoye/mybin/Module_Meta/samtools sort -m 6960000000 Hay_Cecum-1.bam Hay_Cecum-1.sort`  
`/lustre/sdb/taoye/mybin/Module_Meta/samtools index Hay_Cecum-1.sort.bam` 
`/lustre/sdb/taoye/mybin/Module_Meta/metabat/jgi_summarize_bam_contig_depths --outputDepth Hay_Cecum-1.depth Hay_Cecum-1.sort.bam
rm Hay_Cecum-1.bam`  
`/lustre/sdb/taoye/mybin/Module_Meta/metabat/metabat2 -t 40 --inFile Hay_Cecum-1.contigs --abdFile Hay_Cecum-1.depth  --outFile /lustre/sdb/lingen/workB/01.meta/06.BIN/Hay_Cecum-1/Hay_Cecum-1`  
`ls /lustre/sdb/lingen/workB/01.meta/06.BIN/Hay_Cecum-1/Hay_Cecum-1*fa > Hay_Cecum-1.bins.list` 
`cp /lustre/sdb/lingen/workB/01.meta/06.BIN/Hay_Cecum-1/Hay_Cecum-1*fa /lustre/sdb/lingen/workB/01.meta/08.MAGsPorfile/BINs`  
`/lustre/sdb/taoye/miniconda3/bin/checkm lineage_wf /lustre/sdb/lingen/workB/01.meta/06.BIN/Hay_Cecum-1/`   
`/lustre/sdb/lingen/workB/01.meta/06.BIN/Hay_Cecum-1_checkm -x fa -t 40 --pplacer_threads 4 --tab_table -f Hay_Cecum-1.checkm.summary`     

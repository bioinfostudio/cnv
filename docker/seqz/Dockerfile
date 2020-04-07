FROM gcr.io/wise-cycling-267806/cnv
USER root
RUN ln -s /mnt/genome/cnv/results/stage2.seqz.gz /home/bioinfo/cnv/
RUN ln -s /mnt/genome/cnv/results/stage2.seqz.gz.tbi /home/bioinfo/cnv/
RUN chown -R bioinfo:bioinfo /home/bioinfo/cnv
USER bioinfo
WORKDIR /home/bioinfo/cnv/

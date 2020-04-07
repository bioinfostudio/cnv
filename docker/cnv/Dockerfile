FROM gcr.io/wise-cycling-267806/cnv-base
USER root
RUN ln -s /mnt/genome/cnv/results/stage1.seqz.gz /home/bioinfo/cnv/
RUN chown -R bioinfo:bioinfo /home/bioinfo/cnv
USER bioinfo
WORKDIR /home/bioinfo/cnv/

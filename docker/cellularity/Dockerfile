FROM gcr.io/wise-cycling-267806/seqz
USER root
COPY sequenza_results /home/bioinfo/cnv/sequenza_results
RUN chown -R bioinfo:bioinfo /home/bioinfo/cnv
USER bioinfo
WORKDIR /home/bioinfo/cnv/

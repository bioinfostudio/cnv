FROM gcr.io/wise-cycling-267806/cellularity
USER root
WORKDIR /
RUN apt-get update --fix-missing
RUN apt-get install -t buster-backports -y default-jdk
RUN apt-get clean && apt-get purge && rm -rf /var/lib/apt/lists/* /tmp/*
RUN curl -LO https://data.broadinstitute.org/igv/projects/downloads/2.8/IGV_2.8.2.zip \
    && unzip IGV_2.8.2.zip && rm -rf IGV_2.8.2.zip && \
    ln -s /IGV_2.8.2/igvtools /usr/local/bin
USER bioinfo
WORKDIR /home/bioinfo/cnv/

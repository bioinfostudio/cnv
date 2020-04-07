FROM biocontainers/biocontainers:vdebian-buster-backports_cv1
USER root
RUN apt-get update --fix-missing
RUN apt-get install -t buster-backports -y \
    wget \
    curl \
    git \
    build-essential \
    vim \
    man \
    less \
    r-base \
    libxml2-dev \
    libcurl4-openssl-dev \
    python-pip \
    samtools \
    tabix

RUN apt-get clean && apt-get purge && rm -rf /var/lib/apt/lists/* /tmp/*
RUN pip install sequenza-utils
RUN R -e "install.packages('BiocManager')" \
    && R -e "BiocManager::install('copynumber')" \
    && R -e "BiocManager::install('sequenza')"
# create a non-root user
RUN useradd -ms /bin/bash bioinfo
WORKDIR /home/bioinfo/cnv/assets
RUN ln -s /mnt/genome/snv/ref/human_g1k_v37.dict /home/bioinfo/cnv/assets/
RUN ln -s /mnt/genome/snv/ref/human_g1k_v37.fasta /home/bioinfo/cnv/assets/
RUN ln -s /mnt/genome/snv/ref/human_g1k_v37.fasta.fai /home/bioinfo/cnv/assets/
RUN ln -s /mnt/genome/snv/ref/human_g1k_v37.gc50Base.txt.gz /home/bioinfo/cnv/assets/
WORKDIR /home/bioinfo/cnv/data
RUN ln -s /mnt/genome/cnv/data/normal.chr5.60Mb.bam /home/bioinfo/cnv/data/
RUN ln -s /mnt/genome/cnv/data/normal.chr5.60Mb.bam.bai /home/bioinfo/cnv/data/
RUN ln -s /mnt/genome/cnv/data/tumour.chr5.60Mb.bam /home/bioinfo/cnv/data/
RUN ln -s /mnt/genome/cnv/data/tumour.chr5.60Mb.bam.bai /home/bioinfo/cnv/data/
# setup the user directory
RUN chown -R bioinfo:bioinfo /home/bioinfo
RUN echo 'export PS1=" \W\$ "' >> /home/bioinfo/.bashrc
# become the bioinfo
USER bioinfo
ENV HOME /home/bioinfo
WORKDIR /home/bioinfo/

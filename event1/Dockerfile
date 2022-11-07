FROM openanalytics/r-ver:4.1.3

LABEL maintainer="Tobias Verbeke <tobias.verbeke@openanalytics.eu>"

# system libraries of general use
RUN apt-get update && apt-get install --no-install-recommends -y \
    pandoc \
    pandoc-citeproc \
    libcurl4-gnutls-dev \
    libcairo2-dev \
    libxt-dev \
    libssl-dev \
    libssh2-1-dev \
    libssl1.1 \
    && rm -rf /var/lib/apt/lists/*

# system library dependency for the ae app
RUN apt-get update && apt-get install -y \
    libmpfr-dev \
    && rm -rf /var/lib/apt/lists/*

# basic shiny functionality
RUN R -q -e "install.packages(c('shiny', 'rmarkdown'))"

# install dependencies of the ae app
RUN R -q -e "install.packages(c('haven','dplyr','tidyr','gt','shinythemes'),repos='https://cloud.r-project.org/' )"

# copy the app to the image
RUN mkdir /root/ae
COPY ae /root/ae

COPY Rprofile.site /usr/local/lib/R/etc/

EXPOSE 3838

CMD ["R", "-q", "-e", "shiny::runApp('/root/ae')"]

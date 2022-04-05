# ** A base image with python and conda/mamba **
FROM python:3.10-slim-bullseye as python

# Install tini: https://github.com/krallin/tini#why-tini
RUN apt-get update \
 && apt-get install -y \
        tini \
 && rm -rf /var/lib/apt/lists/*
ENTRYPOINT ["tini", "-g", "--"]

# Create a non-root user to run as and switch to it
RUN useradd --create-home --user-group --uid 1000 dask
USER dask:dask
WORKDIR /home/dask/

COPY ./ /tmp/dask-gateway
RUN pip install --no-cache-dir /tmp/dask-gateway

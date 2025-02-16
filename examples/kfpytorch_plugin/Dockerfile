# ######################
# NOTE: For CI/CD only #
########################
FROM python:3.10-slim-buster
LABEL org.opencontainers.image.source https://github.com/flyteorg/flytesnacks

WORKDIR /root
ENV LANG C.UTF-8
ENV LC_ALL C.UTF-8
ENV PYTHONPATH /root
ENV DEBIAN_FRONTEND noninteractive
ENV TERM linux

RUN apt-get update && apt-get install -y make build-essential libssl-dev curl

# Install gcc, g++ and make
RUN apt-get update && apt-get install --no-install-recommends -y gcc g++
RUN echo 'installing make' \
    && apt-get install make

# Virtual environment
ENV VENV /opt/venv
RUN python3 -m venv ${VENV}
ENV PATH="${VENV}/bin:$PATH"

# Install Python dependencies
COPY requirements.txt /root
RUN pip install -r /root/requirements.txt

# Copy the actual code
COPY . /root/

# This tag is supplied by the build script and will be used to determine the version
# when registering tasks, workflows, and launch plans
ARG tag
ENV FLYTE_INTERNAL_IMAGE $tag

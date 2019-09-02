# This Dockerfile was adapted from the one used by the HTMap project

FROM debian:buster-slim

ENV DEBIAN_FRONTEND=noninteractive \
    LC_ALL=en_US.UTF-8 \
    LANG=en_US.UTF-8 \
    LANGUAGE=en_US.UTF-8

# User to submit jobs with
ARG user=dask

# Install
USER root
RUN apt-get update && apt-get -y install htcondor
RUN groupadd ${user} && \
    useradd -m -g ${user} ${user}

# Switch to submitter and finalize
USER ${user}
WORKDIR /home/${user}
COPY ./condor_config.local /etc/condor/condor_config.local
COPY ./entrypoint.sh .
ENTRYPOINT "./entrypoint.sh"

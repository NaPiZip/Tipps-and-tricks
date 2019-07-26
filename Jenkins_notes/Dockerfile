FROM ubuntu:16.04

# Set Bazel version 1
ARG BAZEl=bazel-0.28.1-installer-linux-x86_64.sh

USER root

# Prerequisite: Initial update and wget
RUN apt-get update && apt-get install -y wget

# Step 1: Install required packages
RUN apt-get install -y pkg-config zip g++ zlib1g-dev unzip python3

RUN wget https://github.com/bazelbuild/bazel/releases/download/0.28.1/${BAZEl}

RUN chmod 777 /${BAZEL}

RUN .${BAZEL}

# Create a symlink in /usr/bin that points to /root/bazel
RUN ln -sf /root/.bazel/bin/bazel /usr/bin/

#RUN bazel

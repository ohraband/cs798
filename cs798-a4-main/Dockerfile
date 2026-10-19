# Start from a stock Ubuntu 24.04 image
FROM ubuntu:24.04

# Install Python 3 and basic utilities
RUN apt update && apt install -y python3 python3-pip git && \
    apt clean && rm -rf /var/lib/apt/lists/*

# Copy your a4 code directory into the container
COPY code /root/code/

# Set working directory
WORKDIR /root/code

# Make the a4 script executable
RUN chmod 755 a4

# Default command: open a shell
CMD ["/bin/bash"]

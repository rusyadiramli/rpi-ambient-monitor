FROM resin/rpi-raspbian:jessie
MAINTAINER Maximo Vazquez Brust <chespi@gmail.com>

# Install dependencies
RUN apt-get update && apt-get install -y \
    git-core \
    build-essential \
    gcc \
    python \
    python-dev \
    python-pip \
    python-virtualenv \
    i2c-tools \
    libi2c-dev \
    --no-install-recommends && \
    rm -rf /var/lib/apt/lists/*

RUN pip install requests
RUN pip install rpi.gpio
RUN git clone https://github.com/adafruit/Adafruit_Python_DHT.git
RUN cd Adafruit_Python_DHT && python setup.py install
RUN cd .. && git clone https://github.com/lexruee/tsl2561.git
RUN cd tsl2561 && sudo pip install .
RUN mkdir /project
COPY sense_loop.bash /project/sense_loop.bash
copy sense.py /project/sense.py

# Define working directory
WORKDIR /project

ENTRYPOINT ["/bin/bash", "/project/sense_loop.bash"]

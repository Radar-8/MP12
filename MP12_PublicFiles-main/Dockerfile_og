FROM python:3.6
MAINTAINER CCA

# Creating Application Source Code Directory
RUN apt-get update && \
	apt-get install -y --no-install-recommends build-essential\
	expect git vim zip unzip wget maven sudo
RUN apt-get install -y python3 python3-pip
RUN cd /usr/local/bin;
Run /usr/local/bin/python -m pip install --upgrade pip

# Setting Home Directory for containers
WORKDIR /app

# Installing python dependencies
# copy current files to src folder (requirements.txt and classify.py)
COPY requirements.txt ./
COPY classify.py ./

# install dependencies mentioned in requirements.txt
RUN pip install --no-cache-dir -r requirements.txt

# Application Environment variables. 
# These variables will be used when you run the image. 
# You will also need to pass corresponding DATASET and TYPE variables from the job yaml files of both free-service and default types of jobs.
ENV APP_ENV development
ENV DATASET mnist
ENV TYPE ff

# Exposing Ports
EXPOSE 5035

# Setting Persistent data
VOLUME ["/app-data"]

# Running Python Application (classify.py)
CMD ["python3", "classify.py", "--host", "0.0.0.0", "--port", "5035"]

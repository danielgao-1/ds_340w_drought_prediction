# Pull base image
FROM ubuntu:20.04

# Set environment variables
ENV PYTHONDONTWRITEBYTECODE 1
ENV PYTHONUNBUFFERED 1

ENV TZ=Europe/Moscow
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

# Set work directory
WORKDIR /app

# Install dependencies
COPY requirements.txt /app
RUN apt-get update && apt-get install -y python3 python3-pip libgdal-dev git vim
RUN pip install -r requirements.txt
#for windows, linux 
RUN pip install --force-reinstall torch==1.10.1+cu113 --extra-index-url https://download.pytorch.org/whl/
#for apple 
#RUN pip install --force-reinstall torch==1.10.1 torchvision==0.11.2 torchaudio==0.10.1
# Install GDAL (for preprocessing) 
ARG CPLUS_INCLUDE_PATH=/usr/include/gdal
ARG C_INCLUDE_PATH=/usr/include/gdal
RUN pip3 install gdal==$(gdal-config --version)
# Copy project
COPY . /app/


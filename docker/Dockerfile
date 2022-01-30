FROM nvidia/cuda:11.0-base-ubuntu20.04
#RUN apk add --no-cache tzdata
#ENV TZ Turkey/Istanbul
ENV DEBIAN_FRONTEND=noninteractive
WORKDIR /app

COPY requirements.txt .
COPY lint-requirements.txt .

RUN apt-get -yq update \
     && apt-get upgrade -yq \
     && apt-get -yq install apt-utils gcc libpq-dev libsndfile-dev git sox \
     && apt-get install -yq python3.8 python3.8-dev python3-pip
#     && apt install -y python3-pip \
RUN pip3 install --upgrade pip
RUN pip3 install speechbrain
#RUN ln -sf /usr/bin/python3.8 /usr/bin/python3

RUN pip3 install -r requirements.txt
RUN pip3 install -r  lint-requirements.txt


RUN git clone https://github.com/speechbrain/speechbrain.git
WORKDIR /app/speechbrain/
RUN pip3 install --editable .
#WORKDIR /app/speechbrain

#COPY rest_plus_env_bug.bash .
#COPY service.py  .

#RUN chmod +x rest_plus_env_bug.bash
#RUN ./rest_plus_env_bug.bash

#RUN mkdir /app/models/ /app/inferenceSb/ /app/output/
#ADD ../models /app/models
#ADD ../inferenceSb /app/inferenceSb
#ADD ../output /app/output

#FROM python:3.8.8
#
#EXPOSE 8501
#
#ADD main.py audio_func.py service.py ./
#
#COPY requirements.txt .
#COPY models/ models/
#
#RUN pip install -r requirements.txt
#RUN apt-get update -y && apt-get install -y --no-install-recommends build-essential gcc \
#                                        libsndfile1
#COPY service.py  .
#CMD python service.py -o /outputs

FROM ubuntu:22.04
COPY ./apps /
RUN apt-get update && apt-get install -y \
    software-properties-common
RUN add-apt-repository ppa:deadsnakes/ppa
RUN apt-get update && apt-get install -y \
    python3.9 \
    python3-pip

RUN pip3 install -r /requirements.txt

CMD ["python3", "pop-queue.py"]
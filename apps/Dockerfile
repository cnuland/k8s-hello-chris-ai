FROM ubuntu:14.04
COPY ./apps /
RUN apt-get update && apt-get install -y \
    python3.8 \
    python3-pip

RUN pip install -r /opt/app-root/src/requirements.txt

CMD ["python3", "pop-queue.py"]
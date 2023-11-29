FROM quay.io/jkeam/ubi-python38:latest
COPY ./apps /
RUN pip install -r /opt/app-root/src/requirements.txt

CMD ["python", "pop-queue.py"]
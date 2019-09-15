FROM ubuntu
RUN apt-get update && apt-get install -y \
        default-jdk \
        python
COPY ./docker/backend/penguin-coco-0.0.1-SNAPSHOT.jar app.jar
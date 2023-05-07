# pull official base image
FROM python:3.11.2-slim-buster

# set working directory
WORKDIR /usr/src/app

# set environment variables
ENV PYTHONDONTWRITEBYTECODE 1
ENV PYTHONUNBUFFERED 1

# install system dependencies
RUN apt-get update \
    && apt-get -y install netcat gcc \
    && apt-get clean

# install Poetry
RUN pip3 install --upgrade pip
RUN pip3 install "poetry==1.4.2"

# copy Poetry files
COPY ./pyproject.toml ./poetry.lock ./

# install dependencies
RUN poetry config virtualenvs.create false \
    && poetry install --no-root --no-interaction --no-ansi

# add app
COPY . .

# add entrypoint.sh
COPY ./entrypoint.sh .
RUN chmod +x /usr/src/app/entrypoint.sh

# run entrypoint.sh
ENTRYPOINT ["/usr/src/app/entrypoint.sh"]
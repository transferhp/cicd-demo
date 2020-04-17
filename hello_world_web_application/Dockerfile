FROM python:3

# Creating Application Source Code Directory
RUN mkdir -p /usr/src/app

# Copying src code to Container
COPY . /usr/src/app

# Setting Home Directory for containers
WORKDIR /usr/src/app

# Installing pipenv
RUN pip install pipenv

# Installing python dependencies
RUN pipenv install --system --deploy --ignore-pipfile

# Application Environment variables
#ENV APP_ENV development
ENV PORT 1000

# Exposing Ports
EXPOSE $PORT

# Setting Persistent data
VOLUME ["/app-data"]

# Running Python Application
CMD gunicorn -b :$PORT -c gunicorn.conf.py main:app
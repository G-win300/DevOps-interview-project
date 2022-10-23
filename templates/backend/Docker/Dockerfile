FROM python:3-slim-bullseye
## Upgrade the pip package manager, as it complains otherwise
RUN pip3 install --upgrade pip
COPY setup.py README.md /testserver/
WORKDIR /testserver
## Now let's install the requirements of our little application
RUN pip3 install -e .
## let's add the source code in here
COPY . /testserver
RUN pip3 install -e .
## And let's specify a startup command for docker containers based on this image.
CMD ["sh", "start.sh"]
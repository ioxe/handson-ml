FROM ubuntu:16.04

USER root

RUN apt-get update && apt-get -y install \
  libz-dev \
  cmake \
  python3 \
  python3-dev \
  python3-pip \
  pkg-config

WORKDIR /app

COPY ./requirements.txt requirements.txt

RUN pip3 install --upgrade pip && \
  pip3 install --upgrade -r requirements.txt && \
  pip3 install --upgrade https://github.com/mind/wheels/releases/download/tf1.3-cpu/tensorflow-1.3.0-cp35-cp35m-linux_x86_64.whl && \
  pip3 install jupyter_contrib_nbextensions

WORKDIR /

COPY *.ipynb ./notebooks/

WORKDIR notebooks

COPY datasets ./datasets

COPY images ./images

RUN jupyter contrib nbextension install --user && jupyter nbextension enable toc2/main

CMD ["jupyter", "notebook", "--ip=0.0.0.0", "--no-browser", "--allow-root", "--port=8888", "--notebook-dir=/notebooks", "--NotebookApp.token=''"]

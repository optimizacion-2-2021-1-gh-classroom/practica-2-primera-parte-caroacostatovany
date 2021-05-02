FROM ubuntu:bionic

ENV JUPYTERLAB_VERSION 2.0.0
ENV USER_BINDER jovyan
ENV PIP_PACKAGES_KALE="kubeflow-kale==0.6.1"
RUN apt-get update && export DEBIAN_FRONTEND=noninteractive && echo "America/Mexico_City" > /etc/timezone && apt-get install -y tzdata

RUN apt-get update && apt-get install -y \
	    build-essential \
            sudo \
            nano \
            less \
            git \
            python3-dev \
            python3-pip \
            python3-setuptools \
            nodejs && pip3 install --upgrade pip

RUN groupadd ${USER_BINDER}
RUN useradd ${USER_BINDER} -g ${USER_BINDER} -m -s /bin/bash
RUN echo 'jovyan ALL=(ALL:ALL) NOPASSWD:ALL' | (EDITOR='tee -a' visudo)
RUN echo 'jovyan:qwerty' | chpasswd
RUN pip3 install jupyter jupyterlab==$JUPYTERLAB_VERSION --upgrade
USER ${USER_BINDER}
RUN pip3 install jupyter "jupyterlab>=2.0.0,<3.0.0" --upgrade
RUN pip install $PIP_PACKAGES_KALE --upgrade
RUN pip install --quiet "git+https://github.com/optimizacion-2-2021-1-gh-classroom/practica-1-segunda-parte-caroacostatovany.git#egg=mex&subdirectory=src"
RUN pip install matplotlib
RUN pip install scipy
RUN pip install networkx
RUN pip install pytest

USER root
RUN apt-get update && apt-get install -y sudo nano less git wget curl python3-dev python3-pip python3-setuptools
RUN curl -sL https://deb.nodesource.com/setup_12.x | sudo -E bash - && apt-get install -y nodejs

RUN jupyter notebook --generate-config && sed -i "s/#c.NotebookApp.password = .*/c.NotebookApp.password = u'sha1:115e429a919f:21911277af52f3e7a8b59380804140d9ef3e2380'/" /home/jovyan/.jupyter/jupyter_notebook_config.py
ENV LC_ALL C.UTF-8
ENV LANG C.UTF-8
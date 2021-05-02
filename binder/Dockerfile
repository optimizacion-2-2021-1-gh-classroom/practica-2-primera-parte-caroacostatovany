FROM caroacostatovany/optimizacion-2-practica-2-parte-1:0.1

ARG NB_USER=jovyan
ARG NB_UID=1000
ENV USER ${NB_USER}
ENV NB_UID ${NB_UID}
ENV HOME /home/${NB_USER}
COPY . ${HOME}
USER root
RUN chown -R ${NB_UID} ${HOME}
RUN pip install --no-cache-dir notebook==2.*
RUN pip install --no-cache-dir jupyterhub

USER ${NB_USER}

RUN ["sudo", "chmod", "+x", "/home/jovyan/run.sh"]

ENTRYPOINT ["/home/jovyan/run.sh"]
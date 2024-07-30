FROM image

LABEL org.opencontainers.image.authors="Clement Deltel <clement.deltel@proton.me>"
LABEL org.opencontainers.image.title=""
LABEL org.opencontainers.image.description=""
LABEL com.mycorp.myteam....=""

# Not persisted into the built image
ARG APP_NAME="application"
ARG HOME=
ARG USER="app"
ARG USER_ID="1001"

# Persisted into the built image
ENV HOME="/home/app"
ENV PATH

# Following instructions create a layer: ADD, COPY, RUN
RUN groupadd --gid ${USER_ID} ${USER} && \
    useradd --create-home --home ${HOME} --uid ${USER_ID} --gid ${USER_ID} --comment ${APP_NAME} ${USER}
#--shell /bin/bash

# List packages here
RUN apt-get update -y && \
    apt-get install -y ... && \
    apt-get autoremove -y && \
    apt-get clean

WORKDIR ${HOME}

#ADD only to add files from an URL or tar file
COPY --chown=app src ./src

USER ${USER}

# Default and cannot be overridden
ENTRYPOINT ["/docker-entrypoint.sh"]

# Serve only to container to container communication, does not grant access
# from the host
EXPOSE 80

#STOPSIGNAL SIGQUIT
#HEALTHCHECK --interval=30s --timeout=10s --start-period=30s --retries=3 \
#    CMD ./healthcheck.sh

# Can be overridden by arguments of the docker run command
CMD []

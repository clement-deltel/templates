FROM image

LABEL org.opencontainers.image.authors="Clement Deltel <clement.deltel@proton.me>"
LABEL org.opencontainers.image.title=""
LABEL org.opencontainers.image.description=""
LABEL com.mycorp.myteam....=""

ARG APP_NAME=application
ARG USER_ID="1001"
ARG GROUP_ID="app"
ARG COMMENT="App"
ARG HOME="/app"

ENV APP_NAME=${APP_NAME}
ENV HOME=${HOME}

# Following instructions create a layer: ADD, COPY, RUN
RUN groupadd --gid ${USER_ID} ${GROUP_ID} && \
    useradd --create-home --home /app ${GROUP_ID} --uid ${USER_ID} --gid ${GROUP_ID} --comment ${COMMENT}
#--shell /bin/bash

# List packages here
RUN apt-get update -y && \
    apt-get install -y ... && \
    apt-get autoremove -y && \
    apt-get clean

WORKDIR ${HOME}

#ADD only to add files from an URL or tar file
COPY app/ ${HOME}/${APP_NAME}
ENV PATH $PATH:${HOME}/${APP_NAME}/bin

# Drop root and change ownership of the application folder to the user
#RUN chown -R ${USER_ID}:${GROUP_ID} ${HOME}
# App user only needs execution permissions on the file, not ownership
RUN chmod +x ${HOME}/app.sh
USER ${USER_ID}

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

FROM centos/python-36-centos7:latest

USER root

COPY . /tmp/src

RUN rm -rf /tmp/src/.git* && \
    chown -R 1001 /tmp/src && \
    chgrp -R 0 /tmp/src && \
    chmod -R g+w /tmp/src && \
    rm -rf /tmp/scripts && \
    mv /tmp/src/.s2i/bin /tmp/scripts && \
    rm -rf /opt/app-root/builder/  && \
    cp -rp /tmp/src/builder  /opt/app-root/builder

USER 1001

LABEL io.k8s.description="S2I builder for custom Jupyter notebooks pvc." \
      io.k8s.display-name="Jupyter Notebook Pvc" \
      io.openshift.expose-services="8080:http" \
      io.openshift.tags="builder,jupyter" \
      io.openshift.s2i.scripts-url="image:///opt/app-root/builder"

RUN /tmp/scripts/assemble

CMD [ "/opt/app-root/builder/run" ]

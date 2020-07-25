FROM docker.elastic.co/beats/filebeat:7.6.1

# Patch & update (image scan)
USER root
RUN yum --security check-update -q \
    && yum update -y \
    && yum clean all

USER filebeat
# Copy config files
COPY --chown=root:filebeat files/*.yml /usr/share/filebeat/
COPY --chown=root:filebeat input.config /usr/share/filebeat/input.config

CMD ["filebeat", "-e", "-c", "/usr/share/filebeat/output.elasticsearch.yml", "-c", "/usr/share/filebeat/general.config.yml"]
FROM fluent/fluentd:latest-onbuild

WORKDIR /home/fluent
ENV PATH /home/fluent/.gem/ruby/2.3.0/bin:$PATH

USER root
RUN apk --no-cache add sudo build-base ruby-dev && \
    sudo -u fluent gem install --no-doc fluent-plugin-elasticsearch && \
    rm -rf /home/fluent/.gem/ruby/2.3.0/cache/*.gem && \
    sudo -u fluent gem sources -c && \
    apk del sudo build-base ruby-dev

EXPOSE 24284

USER fluent
CMD exec fluentd -c /fluentd/etc/$FLUENTD_CONF -p /fluentd/plugins $FLUENTD_OPT

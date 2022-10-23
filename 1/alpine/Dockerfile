FROM clojure:alpine
MAINTAINER Forest Keepers <Jeroen.knoops@philips.com>
LABEL description="code-maat docker image."

VOLUME /data

ARG dest=/usr/src/code-maat

RUN mkdir -p $dest
WORKDIR $dest
COPY 1/alpine/code-maat/project.clj $dest
RUN lein deps
COPY 1/alpine/code-maat $dest
RUN mv "$(lein uberjar | sed -n 's/^Created \(.*standalone\.jar\)/\1/p')" app-standalone.jar

ADD REPO .
ADD TAGS .

ENTRYPOINT ["java", "-jar", "app-standalone.jar"]
CMD []

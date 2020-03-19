# Start from a Debian image with the latest version of Go installed
# and a workspace (GOPATH) configured at /go.
FROM golang:latest
# update available packages
RUN apt-get update -y && apt-get upgrade -y && apt install build-essential -y
RUN apt-get install vim -y
# setup dep
RUN curl https://raw.githubusercontent.com/golang/dep/master/install.sh | sh
# create go src directory and clone heimdall
RUN mkdir -p /go/src/github.com/maticnetwork/ \
  && cd /go/src/github.com/maticnetwork/
# change work directory
WORKDIR /go/src/github.com/maticnetwork/
# ADD . /go/src/github.com/maticnetwork/heimdall/
RUN git clone https://github.com/maticnetwork/heimdall.git
# change work directory
WORKDIR /go/src/github.com/maticnetwork/heimdall
# run build
 RUN make build
# GOBIN required for go install
ENV GOBIN $GOPATH/bin
# run build
RUN make install
# initialize heimdall
 RUN heimdalld init
# add volumes
VOLUME ["/root/.heimdalld", "./logs", "./build"]
# expose ports
EXPOSE 1317 26656 26657

FROM golang:1.9.7-stretch
ENV SCOPE_SKIP_UI_ASSETS true
RUN apt-get update && \
	apt-get install -y libpcap-dev python-requests time file shellcheck git curl build-essential python-pip && \
	rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*
RUN go clean -i net && \
	go install -tags netgo std && \
	go install -tags netgo std
RUN curl -fsSL -o shfmt https://github.com/mvdan/sh/releases/download/v1.3.0/shfmt_v1.3.0_linux_amd64 && \
    chmod +x shfmt && \
    mv shfmt /usr/bin
RUN go get -tags netgo \
		github.com/fzipp/gocyclo \
		github.com/golang/lint/golint \
		github.com/kisielk/errcheck \
		github.com/fatih/hclfmt \
		github.com/mjibson/esc \
		github.com/client9/misspell/cmd/misspell && \
	chmod a+wr --recursive /usr/local/go && \
	rm -rf /go/pkg/ /go/src/
RUN pip install yapf==0.16.2 flake8==3.3.0
COPY build.sh /
ENTRYPOINT ["/build.sh"]

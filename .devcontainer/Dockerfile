FROM golang:1.17.6 AS builder

ENV GO111MODULE="on"
ENV GOOS="linux"
ENV GOARCH="arm64"
ENV CGO_ENABLED=0
ENV terraform_version=v1.1.3

RUN git clone https://github.com/hashicorp/terraform.git -b $terraform_version /tmp/terraform && \
    cd /tmp/terraform && \
    go build -o /usr/local/bin && \
    chmod +x /usr/local/bin/terraform

FROM alpine:latest as prod

COPY --from=builder /usr/local/bin/terraform /usr/local/bin/terraform
RUN chmod +x /usr/local/bin/terraform

# Copyright 2016 The Kubernetes Authors All rights reserved.
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#     http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.

FROM --platform=$BUILDPLATFORM golang:1.14.1-alpine3.11 as builder
ARG TARGETPLATFORM

ADD . $GOPATH/src/github.com/kubernetes-retired/peer-finder
WORKDIR $GOPATH/src/github.com/kubernetes-retired/peer-finder

RUN apk add git make
RUN export GOARCH=$(echo $TARGETPLATFORM | sed -e 's|linux/||g' | sed -e 's|/v.*||g') && \
    go get k8s.io/apimachinery/pkg/util/sets && \
    make server && \
    mv peer-finder /

FROM --platform=$TARGETPLATFORM alpine:3.11
MAINTAINER Prashanth.B <beeps@google.com>

RUN apk add wget bash bind-tools
COPY --from=builder /peer-finder /peer-finder
ADD peer-finder.go /peer-finder.go

EXPOSE 9376
ENTRYPOINT ["/peer-finder"]

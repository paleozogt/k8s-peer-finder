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

all: container

TAG = 0.1
PREFIX = paleozogt/k8s-peer-finder

server: peer-finder.go
	CGO_ENABLED=0 go build -a -installsuffix cgo --ldflags '-w' ./peer-finder.go

container:
	docker buildx build --push --platform linux/amd64,linux/arm64,linux/arm,linux/ppc64le,linux/s390x -t $(PREFIX):$(TAG) .

clean:
	rm -f peer-finder

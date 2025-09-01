# Copyright 2019 The Volcano Authors.
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#    http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.

FROM registry-public.lenovo.com/library/golang:1.24-bullseye AS builder
WORKDIR /go/src/volcano.sh/
ENV GOPROXY="https://goproxy.cn,direct"
COPY go.mod go.sum ./
RUN go mod download
ADD . volcano
RUN cd volcano && make vc-scheduler

FROM registry-public.lenovo.com/library/alpine:3.22
COPY --from=builder /go/src/volcano.sh/volcano/_output/bin/vc-scheduler /vc-scheduler
ENTRYPOINT ["/vc-scheduler"]

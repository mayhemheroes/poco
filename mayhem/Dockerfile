# Copyright 2021 Google LLC
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
# http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.
#
################################################################################

FROM gcr.io/oss-fuzz-base/base-builder
# Ubuntu 20.04 (focal) is EOL; fall back to old-releases mirror for reliable package downloads
RUN sed -i "s|http://archive.ubuntu.com/ubuntu|http://old-releases.ubuntu.com/ubuntu|g; s|http://security.ubuntu.com/ubuntu|http://old-releases.ubuntu.com/ubuntu|g" /etc/apt/sources.list 2>/dev/null || true
RUN apt-get -o Acquire::Retries=5 update && apt-get -o Acquire::Retries=5 install -y openssl libssl-dev git make cmake
COPY . poco
RUN rm -rf poco/mayhem
WORKDIR $SRC/poco
COPY mayhem/build.sh mayhem/json_parse_fuzzer.cc $SRC/

ENV FUZZING_LANGUAGE=c++ SANITIZER=address
RUN compile

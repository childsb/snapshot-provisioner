# Copyright 2017 The Kubernetes Authors.
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

FROM centos:7
MAINTAINER bradley childs, bchilds@gmail.com
RUN yum update -y


# Build the AWS CLI and create a bootstrap script
RUN mkdir -p /root/aws_cli
WORKDIR  /root/aws_cli

RUN curl "https://s3.amazonaws.com/aws-cli/awscli-bundle.zip" -o "awscli-bundle.zip"
RUN unzip awscli-bundle.zip
RUN ./awscli-bundle/install -i /usr/local/aws -b /usr/local/bin/aws

# install the shell flex script that the provisioner uses.
RUN mkdir -p  /opt/storage_drivers/flex
COPY flex-provision.sh /opt/storage/scripts/snap-provision.sh

RUN mkdir -p /opt/storage_drivers/provisioners
# install the go kube piece of provisioner
COPY snap-provisioner /opt/storage_drivers/provisioners/snap-provisioner


ENTRYPOINT ["/opt/storage_drivers/provisioners/snap-provisioner"]
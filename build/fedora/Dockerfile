FROM fedora
MAINTAINER \
[Stash <noreply@stashpay.io>]
RUN yum update -y \
 && yum group install -y "Development Tools" "Development Libraries" \
 && yum install -y redhat-rpm-config python3-devel libusbx-devel libudev-devel cmake gcc-c++ \
 && yum remove -y gmp-devel \
 && pip3 install virtualenv \
 && cd ~ \
 && mkdir smt \
 && cd smt \
 && virtualenv -p python3 venv \
 && . venv/bin/activate \
 && pip install --upgrade setuptools \
 && git clone https://github.com/stashpayio/stash-masternode-tool \
 && cd stash-masternode-tool/ \
 && pip install -r requirements.txt \
 && cd ~/smt \
 && set +H \
 && echo "#!/bin/sh" | tee build-smt.sh \
 && echo "cd ~/smt" | tee -a build-smt.sh \
 && echo ". venv/bin/activate" | tee -a build-smt.sh \
 && echo "cd stash-masternode-tool" | tee -a build-smt.sh \
 && echo "git fetch --all" | tee -a build-smt.sh \
 && echo "git reset --hard origin/master" | tee -a build-smt.sh \
 && echo "pip install -r requirements.txt" | tee -a build-smt.sh \
 && echo "pyinstaller --distpath=../dist/linux --workpath=../dist/linux/build stash_masternode_tool.spec" | tee -a build-smt.sh \
 && echo "cd .." | tee -a build-smt.sh \
 && chmod +x build-smt.sh

CMD ~/smt/build-smt.sh

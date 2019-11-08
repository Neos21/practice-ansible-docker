FROM centos:7

# Ansible をインストール・git と一緒に ssh コマンドをインストール
RUN set -x && \
    yum install -y ansible git

# ホストチェックを無効化する
ENV ANSIBLE_HOST_KEY_CHECKING False

CMD ["/bin/bash"]

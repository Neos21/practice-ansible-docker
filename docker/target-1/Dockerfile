FROM centos:7

# OpenSSH をインストール・鍵ペアを作成・root ユーザでの SSH ログインを許可する
# - 鍵ペアを3種類作らないと `/usr/sbin/sshd -D` 実行時に `Could not load host key:` といわれる
# - 操作前後の内容を出力するための grep を仕込んでいる
RUN set -x && \
    yum -y install openssh-server && \
    ssh-keygen -t rsa -N '' -f /etc/ssh/ssh_host_rsa_key && \
    ssh-keygen -t ecdsa -N '' -f /etc/ssh/ssh_host_ecdsa_key && \
    ssh-keygen -t ed25519 -N '' -f /etc/ssh/ssh_host_ed25519_key && \
    grep 'PermitEmptyPasswords' /etc/ssh/sshd_config && \
    sed -r -i 's/^#PermitEmptyPasswords no/PermitEmptyPasswords yes/' /etc/ssh/sshd_config && \
    grep 'PermitEmptyPasswords' /etc/ssh/sshd_config && \
    grep 'root' /etc/shadow && \
    echo 'root:mypassword' | chpasswd && \
    grep 'root' /etc/shadow

# SSH ポートを公開する
EXPOSE 22

# sshd を起動する
CMD ["/usr/sbin/sshd", "-D"]

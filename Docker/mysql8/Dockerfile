FROM mysql:8.0.20

# カスタマイズしたローカルのmy.cnfを含める
ADD ./Docker/mysql8/etc/mysql/conf.d/my.cnf /etc/mysql/conf.d/my.cnf

# my.cnfは644でないと無視されてしまうため、パーミッションを変更
RUN chmod 644 /etc/mysql/conf.d/my.cnf

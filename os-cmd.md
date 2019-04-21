# 현재 열려있는 포트를 확인
netstat -tulpn | grep LISTEN

# CentOS6까지만 동작했던 명령입니다.
service iptables status

# CentOS7에서 방화벽 iptables 현황을 볼 수 있습니다.
iptables -L --line

# 포트가 외부에서 접속되지 않는다면 포트를 방화벽에 추가합니다.
sudo firewall-cmd --zone=public --add-port=8000/tcp --permanent

# 방화벽을 리로드합니다.
sudo firewall-cmd --reload

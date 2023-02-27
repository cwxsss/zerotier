#!/bin/bash 
# centos自动安装zerotier 并设置的为planet服务器
# addr服务器公网ip+port
 ip=`wget http://ipecho.net/plain -O - -q ; echo`
 addr=$ip/9993

 echo "********************************************************************************************************************"
 echo "**********centos自动安装zerotier 并设置的为planet服务器 火木木制作 放在root目录执行**********************************"
curl -s https://install.zerotier.com | bash
 yum install gcc gcc-c++ -y
 yum install git -y
cd /opt && git clone -v https://gitee.com/opopop880/ZeroTierOne.git --depth 1 
cd /var/lib/zerotier-one && zerotier-idtool initmoon identity.public >moon.json
cd / && git clone https://gitee.com/opopop880/docker-zerotier-planet.git
mv ./docker-zerotier-planet ./app
  echo "{
  \"stableEndpoints\": [
    \"$ip/9993\"
  ]
}
" >/app/patch/patch.json
cd /app/patch && python3 patch.py 
cd /var/lib/zerotier-one && zerotier-idtool genmoon moon.json && mkdir moons.d && cp ./*.moon ./moons.d
cd /opt/ZeroTierOne/attic/world/ && sh build.sh
sleep 8s
cd /opt/ZeroTierOne/attic/world/ && ./mkworld
mkdir /app/bin -p && cp world.bin /app/bin/planet
cd /app/bin/
\cp -r ./planet /var/lib/zerotier-one/
\cp -r ./planet /root
systemctl restart zerotier-one.service
wget https://gitee.com/opopop880/ztncui/attach_files/932633/download/ztncui-0.8.6-1.x86_64.rpm
rpm -ivh ztncui-0.8.6-1.x86_64.rpm
cd /opt/key-networks/ztncui/
echo 'HTTP_PORT=3443' >.env
echo 'NODE_ENV=production' >>.env
echo 'HTTP_ALL_INTERFACES=true' >>.env
systemctl restart ztncui
rm -rf /opt/ZeroTierOne
echo "**********安装成功*********************************************************************************"

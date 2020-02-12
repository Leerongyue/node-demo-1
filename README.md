# ssh 远程登录
```
echo '复制本地~/.ssh/id_rsa.pub内容' >> ~/.ssh/authorized_keys
```
# 防止 ssh 卡住
```
echo "Host *" >> /etc/ssh/ssh_config
echo "  ServerAliveInterval 30" >> /etc/ssh/ssh_config
```

# 创建应用账户
```
adduser frank
mkdir  /home/frank/.ssh
cp ~/.ssh/authorized_keys /home/frank/.ssh/
chmod 755 /home/frank/.ssh/authorized_keys
chown frank:frank /home/frank/.ssh/authorized_keys

adduser frank sudo
```
# 安装 Node.js 8
```
curl -sL https://deb.nodesource.com/setup_8.x | sudo bash -
sudo sed -i 's/deb.nodesource.com\/node_8.x/mirrors.tuna.tsinghua.edu.cn\/nodesource\/deb_8.x/g' /etc/apt/sources.list.d/nodesource.list
sudo apt-get update
sudo apt-get install -y nodejs
node -v
npm -v
npx -v

sudo apt install git
```
# 部署应用
```
git clone https://github.com/FrankFang/nodejs-test.git
cd nodejs-test
touch log
启动命令：node server.js 8888 > log 2>&1 &
//////////////////////////////////////
把启动命令做成 start 文件
touch start
echo 'node server.js 8888 > log 2>&1 &' >> ./start
添加执行权限 chmod +x ./start
运行 sh ./start 得到一个进程号 pid
//////////////////////////////////////
tail log 看 log 内容
kill -9 pid 可以关掉进程
killall node 可以关掉所有 node 进程
```
# 如何重启应用
```
ssh frank@实例ip
cd nodejs-test
git pull
killall node（因为忘了进程号，实际上可以记下来）
sh ./start
```


## keep oracle vps alive 甲骨文保活脚本

### 选择个根目录/或者家目录home
### 创建 keeporaclealive 目录并新建 docker-compose.yml 文件，复制以下配置文件。
```
mkdir keeporaclealive
cd keeporaclealive
vi docker-compose.yml

version: '3'
services:
  keeporaclealive:
    image: alpine
    command: 'sh -c "while true; do for i in $$(seq 1 100000); do j=$$[i*i]; done; done"'
restart: always
```
### 启动关闭手动测试
### 启动，如报错没有docker，根据提示安装即可
```
docker-compose up -d
```
### 停止
```
docker-compose down
```



### 利用crontab定时运行，添加以下两条记录，注意修改相应的语句
```
crontab -e
```

```
1，11，21，31，41，51 * * * * cd /home（自己的目录）/keeporaclealive && /usr/local（ubuntu可用，centos要修改）/bin/docker-compose up -d
2，12，22，32，42，52 * * * * cd /home（自己的目录）/keeporaclealive && /usr/local（ubuntu可用，centos要修改）/bin/docker-compose down
```

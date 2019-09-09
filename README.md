# rocketmq-docker
重新弄了下

参考了https://github.com/FengRi/rocketmq-docker

# 配置hosts文件 (注意修改ip)(域名在.env文件中)

    192.168.0.7 namesrv.rocketmq.com
    192.168.0.7 m.a.broker.rocketmq.com
    192.168.0.7 s.a.broker.rocketmq.com
    192.168.0.7 m.b.broker.rocketmq.com
    192.168.0.7 s.b.broker.rocketmq.com
    修改.env文件中的ROCKETMQ_HM_HOST的IP

# RocketMQ base

    可以根据需要调整RocketMQ 内存参数(base/Dockerfile)

# RocketMQ 4.5.0

    docker-compose up -d
    
# 测试一下
root@victor:/opt# docker ps|grep rocketmq-broker
004ffb7c04c9        rocketmq-broker-b-s:4.5.0   "/bin/sh -c 'sh mqbr…"   13 minutes ago      Up 13 minutes       0.0.0.0:21909->21909/tcp, 0.0.0.0:21911->21911/tcp   rocketmq-450_rocketmq-broker-b-s_1
cdf20e68d2dc        rocketmq-broker-a-s:4.5.0   "/bin/sh -c 'sh mqbr…"   13 minutes ago      Up 13 minutes       0.0.0.0:11909->11909/tcp, 0.0.0.0:11911->11911/tcp   rocketmq-450_rocketmq-broker-a-s_1
cc88b81f8dba        rocketmq-broker-a-m:4.5.0   "/bin/sh -c 'sh mqbr…"   13 minutes ago      Up 13 minutes       0.0.0.0:10909->10909/tcp, 0.0.0.0:10911->10911/tcp   rocketmq-450_rocketmq-broker-a-m_1
5d42be2889dd        rocketmq-broker-b-m:4.5.0   "/bin/sh -c 'sh mqbr…"   13 minutes ago      Up 13 minutes       0.0.0.0:20909->20909/tcp, 0.0.0.0:20911->20911/tcp   rocketmq-450_rocketmq-broker-b-m_1

root@victor:/opt# docker exec -it 004ffb7c04c9  ./mqadmin clusterList -n 192.168.0.7:9876
OpenJDK 64-Bit Server VM warning: ignoring option PermSize=128m; support was removed in 8.0
OpenJDK 64-Bit Server VM warning: ignoring option MaxPermSize=128m; support was removed in 8.0
#Cluster Name     #Broker Name            #BID  #Addr                  #Version                #InTPS(LOAD)       #OutTPS(LOAD) #PCWait(ms) #Hour #SPACE
DefaultCluster    broker-a                0     192.168.0.7:10911      V4_5_0                   0.00(0,0ms)         0.00(0,0ms)          0 435518.65 -1.0000
DefaultCluster    broker-a                1     192.168.0.7:11911      V4_5_0                   0.00(0,0ms)         0.00(0,0ms)          0 435518.65 0.0319
DefaultCluster    broker-b                0     192.168.0.7:20911      V4_5_0                   0.00(0,0ms)         0.00(0,0ms)          0 435518.65 -1.0000
DefaultCluster    broker-b                1     192.168.0.7:21911      V4_5_0                   0.00(0,0ms)         0.00(0,0ms)          0 435518.65 0.0319

RocketMQ Console (注意修改ip)

    docker run -d -e "JAVA_OPTS=-Drocketmq.namesrv.addr=192.168.0.7:9876 -Dcom.rocketmq.sendMessageWithVIPChannel=false" -p 12345:8080 -t styletang/rocketmq-console-ng
    
 

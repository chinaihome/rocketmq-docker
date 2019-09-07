# rocketmq-docker
有坑，重新弄了下

参考了https://github.com/FengRi/rocketmq-docker

配置hosts文件 (注意修改ip)(域名在.env文件中)

    192.168.0.7 namesrv.rocketmq.com
    192.168.0.7 m.a.broker.rocketmq.com
    192.168.0.7 s.a.broker.rocketmq.com
    192.168.0.7 m.b.broker.rocketmq.com
    192.168.0.7 s.b.broker.rocketmq.com
    修改.env文件中的ROCKETMQ_HM_HOST的IP

RocketMQ base

    可以根据需要调整RocketMQ 内存参数(base/Dockerfile)

RocketMQ 4.5.0

    docker-compose up -d

RocketMQ Console (注意修改ip)

    docker run -d -e "JAVA_OPTS=-Drocketmq.namesrv.addr=192.168.0.7:9876 -Dcom.rocketmq.sendMessageWithVIPChannel=false" -p 12345:8080 -t styletang/rocketmq-console-ng

# HTTP2

专注于性能方面的问题

# 减少协议的大小

1. 通过encoder压缩头部信息。
2. 通讯双方各自cache一份header fields表，不发送重复信息
3. 对HTTP协议使用二进制解析，原本是文本解析
4. 每个http request会生成自己的stream，一个TCP连接上可存在多个stream
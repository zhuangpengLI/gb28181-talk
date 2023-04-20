# gb28181-talk
- 支持私网对讲 走udp
- 支持公网网对讲 走rtp 被动模式
- 需要国标语音对讲可以私聊,QQ:90834938
- wx：a7491772

# 实现方式（配合jessibuca播放器）：
1. 用webrtc推流给zlmediakit.
2. sip控制设备双向对讲。
3. 调用zlmediakit的startSendRtp接口(指定recv_stream_id参数)，把webrtc推流的这路流再推给设备。
4. 设备发送rtp给zlmediaikit startSendRtp接口创建的端口(也就是用于发送和接收rtp的端口)。
5. zlmediakit收到设备发送的rtp，生成新的一路流，流id为recv_stream_id参数指定。
6. 使用webrtc协议或其他协议播放rtp/recv_stream_id这路流。

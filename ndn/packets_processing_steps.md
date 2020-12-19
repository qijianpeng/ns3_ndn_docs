# ndnSIM中数据处理流程

1. App 发送数据包(以`Interest`为例), 调用`AppLinkService::onReceiveInterest`进入转发流程;
2. `AppLinkService::onReceiveInterest`调用父类实现`LinkService::receiveInterest`触发信号;
3. `afterReceiveInterest` 通知`Face.afterReceiveInterest`(在Face实例化时绑定了监听事件);
4. `Face.afterReceiveInterest`触发`Forwarder::startProcessInterest`流程, 其绑定过程也是`Forwarder`
   实例化的时候:
   ```cpp
    face.afterReceiveInterest.connect(
      [this, &face] (const Interest& interest, const EndpointId& endpointId) {
        this->startProcessInterest(FaceEndpoint(face, endpointId), interest);
    });
   ```
5. `Forwarder`调用`Strategy::afterReceiveInterest`进入转发策略;
6. `Strategy`根据策略,进入`Forwarder::onOutgoingInterest`流程(在本地没有`Data`命中的情况下);
7. `Forwarder::onOutgoingInterest`调用出口`egress.face.sendInterest`;
8. 进入`LinkService::sendInterest`, 调用`GenericLinkService::doSendInterest`;
9. 将`Data`进行处理(如分片), 转换为`Block`;
10. 调用`Transport::send`发送数据(在ndnSIM中, `Transport`的实现是`NetDeviceTransport`);
11. 调用`PointToPointNetDevice::Send`发送数据, 由此进入了NS3的数据转发流程.

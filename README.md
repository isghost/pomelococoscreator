# pomelococoscreator
专为cocos creator修改的pomelo游戏框架的客户端js代码，使用的是websocket协议，服务端初始化时，通讯类型选第一个(ws)
# 源文件列表及地址
* [protocol](https://github.com/NetEase/pomelo-protocol)
* [protobuf](https://github.com/pomelonode/pomelo-protobuf)
* [pomelo-jsclient-websocket](https://github.com/pomelonode/pomelo-jsclient-websocket)

# 修改内容
将上面的文件直接扔进工程，是无法直接使用`pomelo`，需要做一些简单修改，修改后的文件放在
[pomelo](https://github.com/isghost/pomelococoscreator/tree/master/pomelo)这里。将代码丢进工程,
再```require("relative_path/pomelo-client")```即可。

# 使用方法
以下内容引用自[pomelo-jsclient-websocket](https://github.com/pomelonode/pomelo-jsclient-websocket)

## 连接到服务器

	pomelo.init(params, callback);

例子:

	pomelo.init({
		host: host,
		port: port,
		user: {},
		handshakeCallback : function(){}
	}, function() {
		console.log('success');
	});
	//@param user 发送给服务器的json串
	//@param handshakeCallback 握手回调

## 发送`request`到服务器

	pomelo.request(route, msg, callback);

例子:

    pomelo.request(route, {
        rid: rid
    }, function(data) {
    	console.log(dta);   
    });

## 发送`request`到服务器没有回调，即通知(notify)。

	pomelo.notify(route, params);

## 从服务器接收消息，即推送(push)。

	pomelo.on(route, callback);

例子:

    pomelo.on('onChat', function(data) {
        addMessage(data.from, data.target, data.msg);
        $("#chatHistory").show();
    });

## 断开连接

	pomelo.disconnect();

# 异常

以下内容为查看源码所得，不保证正确性

## 异常触发的事件

	pomelo.emit('reconnect');
	pomelo.emit('io-error', event);
	pomelo.emit('close',event);
	pomelo.emit('disconnect', event);
	pomelo.emit('heartbeat timeout');
	pomelo.emit('error', 'client version not fullfill');
	pomelo.emit('error', 'handshake fail');
	pomelo.emit('onKick', data);

## 设置异常事件处理(事件名对应即可)

	pomelo.on("reconnect", callback);

	pomelo.on("close",  function(event){
		
	});

	pomelo.on("io-error", function(event){

	});

## 异常事件状态码
由于`close`事件可以是正常关闭，也有可能是异常关闭，所以需要根据关闭时，事件的`code`进行相应的处理
状态码查询地址： [MDN](https://developer.mozilla.org/en-US/docs/Web/API/CloseEvent)

需要注意的是，socket的error事件对应pomelo的事件是io-error。
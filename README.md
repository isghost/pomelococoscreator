# pomelococoscreator
专为cocos creator修改的pomelo-jsclient代码

# 源文件列表及地址
* [protocol](https://github.com/NetEase/pomelo-protocol)
* [protobuf](https://github.com/pomelonode/pomelo-protobuf)
* [pomelo-jsclient-websocket](https://github.com/pomelonode/pomelo-jsclient-websocket)

# 修改内容
将上面的文件直接扔进工程，是无法直接使用`pomelo`，需要做一些简单修改，修改后的文件放在
[pomelo](https://github.com/isghost/pomelococoscreator)这里。将代码丢进工程,
再```require("relative_path/pomelo")```即可。

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
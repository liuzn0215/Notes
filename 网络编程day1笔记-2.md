

---
#获取开源代码的网站
* code.google.com
* github.com
* 在github搜索smart-image-view
* 下载开源项目smart-image-view
* 使用自定义组件时，标签名字要写包名

		<com.loopj.android.image.SmartImageView/>
* SmartImageView的使用

		SmartImageView siv = (SmartImageView) findViewById(R.id.siv);
		siv.setImageUrl("http://192.168.1.102:8080/dd.jpg");

---
#Html源文件查看器
* 发送GET请求

		URL url = new URL(path);
		//获取连接对象
		HttpURLConnection conn = (HttpURLConnection) url.openConnection();
		//设置连接属性
		conn.setRequestMethod("GET");
		conn.setConnectTimeout(5000);
		conn.setReadTimeout(5000);
		//建立连接，获取响应吗
		if(conn.getResponseCode() == 200){
				
		}
* 获取服务器返回的流，从流中把html源码读取出来

		byte[] b = new byte[1024];
		int len = 0;
		ByteArrayOutputStream bos = new ByteArrayOutputStream();
		while((len = is.read(b)) != -1){
			//把读到的字节先写入字节数组输出流中存起来
			bos.write(b, 0, len);
		}
		//把字节数组输出流中的内容转换成字符串
		//默认使用utf-8
		text = new String(bos.toByteArray());
###乱码的处理
* 乱码的出现是因为服务器和客户端码表不一致导致
		
		//手动指定码表
		text = new String(bos.toByteArray(), "gb2312");

---
#提交数据
###GET方式提交数据
* get方式提交的数据是直接拼接在url的末尾

		final String path = "http://192.168.1.104/Web/servlet/CheckLogin?name=" + name + "&pass=" + pass;

* 发送get请求，代码和之前一样

		URL url = new URL(path);
		HttpURLConnection conn = (HttpURLConnection) url.openConnection();
		conn.setRequestMethod("GET");
		conn.setReadTimeout(5000);
		conn.setConnectTimeout(5000);
		if(conn.getResponseCode() == 200){

		}
* 浏览器在发送请求携带数据时会对数据进行URL编码，我们写代码时也需要为中文进行URL编码

		String path = "http://192.168.1.104/Web/servlet/CheckLogin?name=" + URLEncoder.encode(name) + "&pass=" + pass;
###POST方式提交数据
* post提交数据是用流写给服务器的
* 协议头中多了两个属性
	* Content-Type: application/x-www-form-urlencoded，描述提交的数据的mimetype
	* Content-Length: 32，描述提交的数据的长度

			//给请求头添加post多出来的两个属性
			String data = "name=" + URLEncoder.encode(name) + "&pass=" + pass;
			conn.setRequestProperty("Content-Type", "application/x-www-form-urlencoded");
			conn.setRequestProperty("Content-Length", data.length() + "");

* 设置允许打开post请求的流

		conn.setDoOutput(true);

* 获取连接对象的输出流，往流里写要提交给服务器的数据

		OutputStream os = conn.getOutputStream();
		os.write(data.getBytes());



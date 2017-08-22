### FileDownloader

* 一个简单的断点下载工具类
* 使用线程池，初始线程数为0，最大线程数Integer.MAX_VALUE，线程空闲60秒后自动回收
* 可以中断下载，下载自动断点下载

### 使用方法

##### 下载
```
String downLoadUrl = "http://liyafeng.com/startActivity.png";
//下载到sd卡中的 /Android/data/包名/files/目录下
File externalFilesDir = context.getExternalFilesDir(null);
String storagePath = new File(externalFilesDir,"file.png").getAbsolutePath();
FileDownLoader.getInstance().start(context, downLoadUrl, storagePath, new FileDownLoader.IDownloadListener() {
			@Override
			public void progress(int soFarBytes, int totalBytes) {
		      //开始下载
					float current = ((int) (soFarBytes / 1024.0f / 1024 * 10)) / 10f;
					float total = ((int) (totalBytes / 1024.0f / 1024 * 10)) / 10f;
					int i = (int) (current * 100 / total);
			    //i为下载百分比
				
			}

			@Override
			public void completed() {
			   //下载完成
			}

			@Override
			public void error(Exception e) {
				String msg = "error: ";
				if (e != null) {
					msg += e.getMessage();
				}
				//下载出错，如果断网也会在这抛出异常
			}

			@Override
			public void start() {
				//开始建立下载连接
			}
		});
```
##### 取消所有下载
```
FileDownLoader.getInstance().stopAll();
```
##### 取消单个Url的下载
```
FileDownLoader.getInstance().stopDownLoad("http://liyafeng.com/startActivity.png");
```

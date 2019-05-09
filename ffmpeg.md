1.下载
ffmpeg官网：官网，我下载的是最新版本，3.2.4

tar -xjf ffmpeg-3.2.4.tar.bz2  //解压命令
1
2.安装依赖库
sudo apt-get install libx264-dev  //这个比较关键，因为在编码的时候依赖这个库
1. sudo apt-get install libfaac-dev
2. sudo apt-get install libmp3lame-dev
3. sudo apt-get install libtheora-dev
4. sudo apt-get install libvorbis-dev
5. sudo apt-get install libxvidcore-dev
6. sudo apt-get install libxext-dev
7. sudo apt-get install libxfixes-dev
1
2
3
4
5
6
7
8
3.配置、编译 ffmpeg
./configure --enable-gpl --enable-version3 --enable-nonfree --enable-postproc  --enable-pthreads  --enable-libmp3lame --enable-libtheora --enable-libx264 --enable-libxvid --enable-x11grab --enable-libvorbis --enable-shared --prefix=/usr/local/ffmpeg --disable-yasm
//prefix表示安装的目录
//disable-yasm表示禁用yasm

make   //然后编译，比较慢
sudo make install  //安装
1
2
3
4
5
6
4.环境配置
安装完成后在/usr/local/ffmpeg下出现三个目录 
bin，lib,include 
为了能够使程序找到动态库 
可以在/etc/ld.so.conf.d/目录下来创建一个新的文件ffmpeg.conf 
文件中包含一句话：

/usr/local/ffmpeg/lib
1
然后运行：

sudo ldconfig   //更新ld.so.cache，使修改生效
1
为了在任何地方都可以直接用ffmpeg运行，不用使用./ffmpeg 
，可以将可执行程序复制到bin目录下

sudo cp /usr/local/ffmpeg/bin/ffmpeg /usr/local/bin/ 
sudo cp /usr/local/ffmpeg/bin/ffprobe /usr/local/bin/ 
sudo cp /usr/local/ffmpeg/bin/ffserver /usr/local/bin/
1
2
3
至此安装完成，可以运行

sudo ffmpeg //如果出现版本信息说明安装成功
1
5.ffmpeg简单命令
1.视频转换

ffmpeg -i input.avi output.mp4
1
2
2.视频编码格式转化 
将avi转换成H.264格式的mp4视频格式

ffmpeg -i inputfile.avi -f mp4　-acodec libfaac -vcodec libx264 outputfile.mp4 
1
3，视频的分辨率改变

ffmpeg -i input.avi -s 1280*720 output.avi
--------------------- 
作者：shitangdejiaozi 
来源：CSDN 
原文：https://blog.csdn.net/shitangdejiaozi/article/details/59110384 
版权声明：本文为博主原创文章，转载请附上博文链接！
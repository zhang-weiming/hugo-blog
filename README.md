# 张大锅的博客

1. 克隆博客代码文件
    ```shell
    git clone https://github.com/zhang-weiming/zhang-weiming.github.io.git
    cd zhang-weiming.github.io
    ```
2. 下载主题
    ```shell
    git clone https://github.com/hugo-fixit/FixIt.git themes/FixIt
    git clone https://github.com/Lruihao/hugo-shortcode-sponsor-log.git themes/shortcode-sponsor-log
    ```

3. 运行
    ```shell
    hugo server -D --bind <本机IP> --baseURL=http://<本机IP>
    ```
4. 编译静态页面
    ```shell
    hugo
    ```

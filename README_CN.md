# 使用 Redis 实现视觉和语义的相似性

此演示与 [Redis 向量相似性搜索的公告](https://redis.com/blog/build-intelligent-apps-redis-vector-similarity-search/) 一起进行

您将使用真实的数据集试验矢量相似性搜索应用程序的两个关键应用程序：

* 语义搜索：给定一个句子，检查产品关键字中具有语义相似文本的产品
* 视觉搜索：给定一个查询图像，在目录中找到最“视觉上”相似的前 K 个

# 关于亚马逊产品数据集

本演示中使用的 CSV 产品数据来自 [“Amazon Berkeley Objects Dataset”](https://amazon-berkeley-objects.s3.amazonaws.com/index.html)

CSV 文件中的每一行对应于原始数据集中的一个产品。

![7MOIOm](https://oss.images.shujudaka.com/uPic/7MOIOm.png)


# 在你开始之前

* 安装 Git

    * [安装手册](https://git-scm.com/book/zh/v2/%E8%B5%B7%E6%AD%A5-%E5%AE%89%E8%A3%85-Git)

* 安装 [Git LFS](https://git-lfs.github.com/)

     * 确保通过运行来初始化 LFS
     ```
     git lfs 安装
     ```
* 安装 Docker

* [安装 Docker Compose](https://docs.docker.com/compose/install/)

# 克隆仓库

```
git clone https://github.com/RedisAI/vecsim-demo.git
```

# 启动 Docker 容器

使用 docker-compose 启动 2 个容器：
* vesim：在端口 6379 上具有矢量相似性搜索 (VSS) 的 redis 容器
* jupyter: 8888 端口上预装了 4 个笔记本的 Python 笔记本服务器
     * 2 个说明如何使用 Redis VSS 执行视觉相似性的笔记本
     * 2 个说明如何使用 Redis VSS 执行语义相似性的笔记本

```
cd vecsim-demo
docker-compose up
```

**注意**：第一次运行上述命令时，需要 5-10 分钟（取决于您的网络）
jupyter 容器从 [“Amazon Berkeley Objects Dataset”](https://amazon-berkeley-objects.s3.amazonaws.com/index.html) 下载带有产品图像的 3.25GB tar 文件

# 启动 Jupyter 笔记本

监控日志并查找在本地计算机上启动 jupyter 的链接

![复制网址](./docs/jupyter-log.png)

打开本地浏览器到此链接


# 第 1 步：语义相似性 - 第一部分

打开这个笔记本 [http://127.0.0.1:8888/notebooks/SemanticSearch1k.ipynb](http://127.0.0.1:8888/notebooks/SemanticSearch1k.ipynb)

运行所有单元并检查输出

您将为 1,000 个产品生成嵌入并使用两种索引方法（HNSW 和 brute-force）执行语义相似性

# 第 2 步：语义相似性 - 第二部分

打开这个笔记本 [http://127.0.0.1:8888/notebooks/SemanticSearch100k.ipynb](http://127.0.0.1:8888/notebooks/SemanticSearch100k.ipynb)

运行所有单元并检查输出

您将为数据集中的前 100,000 个产品加载约 100k 先前生成的嵌入。

您将在更大的数据集上执行语义相似性

# 第 3 步：视觉相似性 - 第一部分

打开这个笔记本 [http://127.0.0.1:8888/notebooks/VisualSearch1k.ipynb](http://127.0.0.1:8888/notebooks/VisualSearch1k.ipynb)

运行所有单元并检查输出

您将为 1,000 个产品图像生成嵌入，并使用两种索引方法执行视觉相似性

# 第 4 步：视觉相似性 - 第二部分

打开这个笔记本 [http://127.0.0.1:8888/notebooks/VisualSearch100k.ipynb](http://127.0.0.1:8888/notebooks/VisualSearch100k.ipynb)

您将使用两种索引方法（HNSW 和 brute-force）对更大的数据集执行视觉相似性

# 停止 Docker 容器

```
docker-compose down
```

# 关于亚马逊产品数据

本演示中使用的数据集来自 ["Amazon Berkeley Objects Dataset"](https://amazon-berkeley-objects.s3.amazonaws.com/index.html)

特别是，product_data.csv 中的每个长文本字段都是从表示每个产品的原始 JSON 编码对象中提取的。

感谢 Amazon.com 分享原始数据集。 这包括 [Creative Commons Attribution-NonCommercial 4.0 International Public License (CC BY-NC 4.0)](https://creativecommons.org/licenses/by-nc/4.0/) 下的所有产品数据、图像和 3D 模型

Credit to the creators of the dataset: 
Matthieu Guillaumin Amazon.com 
Thomas Dideriksen Amazon.com 
Kenan Deng Amazon.com 
Himanshu Arora Amazon.com 
Arnab Dhua Amazon.com 
Xi (Brian) Zhang Amazon.com 
Tomas Yago-Vicente Amazon.com 
Jasmine Collins UC Berkeley 
Shubham Goel UC Berkeley 
Jitendra Malik UC Berkeley

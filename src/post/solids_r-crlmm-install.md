title = "安装一个R包的艰难旅程"
datetime = "2013-10-14 18:30"
tags=["[solids]","生物信息","R","软件","包"]

-------------------

好不容易为SNP数据找到这个包[crlmm](http://www.bioconductor.org/packages/2.12/bioc/html/crlmm.html)

然后经历了以下阶段：

- 按说明手册来装

```R 
source("http://bioconductor.org/biocLite.R")
biocLite("crlmm")
``` 

  ERROR: dependency ‘DBI’ is not available for package ‘RSQLite’

  错误：没有DBI包

- 去装DBI

```R
  install.packages("~/pro/packages/R/DBI_0.2-7.tar.gz")
```

  错误：R的版本是2.14.1，程序包'DBI'要求版本为>= 2.15.0的R

- 升级R 至3.0.2

  
   [3.0.2包](http://www.cnblogs.com/emanlee/p/3349650.html)
   [安装方法](http://isnailbook.com/archives/131)

```sh
wget http://cran.rstudio.com/src/base/R-3/R-3.0.2.tar.gz
tar xzvf R-3.0.2.tar.gz
cd R-3.0.2
./configure
```

  error: with-readline=yes (default) and headers/lib are not available

   [参考](http://stackoverflow.com/questions/17637164/error-with-readline-yes-default-and-headers-lib-are-not-available)
  
```sh
./configure --with-x=no --with-readline=no
make
sudo make install
```

- 再按最开始来，中间终于没报错了

**撒花！**

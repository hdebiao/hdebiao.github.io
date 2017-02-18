---
layout:     post
title:      生成一个安全的随机数
date:       2017-02-17
author:     HDB
header-img: img/post-bg-re-vs-ng2.jpg
catalog: true
tags:
    - php
---



## 生成一个安全的随机数

* php 通过读取linux 下的/dev/urandom 设备获取安全的随机数

* 微信小程序推荐使用16B的随机数 也就是128位

~~~
   //获取安全的随机字符串

    public function getSafetyRandomString()
    {
        $random_string = '';
        try {
            $fp = @fopen('/dev/urandom', 'r');
            if ($fp !== false) {
                $random_string .= @fread($fp, 16);
                $pr_bits_arr = unpack('H*', $random_string);
                $random_string = $pr_bits_arr[1];
                @fclose($fp);
            }

        } catch (\Exception $e) {
            error_log($e->getMessage());
        }
        return $random_string;
    }
    
    //得到的结果如  :  063060b430eea54f49b8795aeaa08038 
    
~~~
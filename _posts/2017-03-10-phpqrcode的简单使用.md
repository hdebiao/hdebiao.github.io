---
layout:     post
title:      phpqrcode的简单使用
date:       2017-03-10
author:     HDB
header-img: img/post-bg-re-vs-ng2.jpg
catalog: true
tags:
    - php
---



[phpqrcode官网](http://phpqrcode.sourceforge.net/)

## 向浏览器输出二维码

```
<?php

include_once './phpqrcode.php';

header('Content-Type:image/png');

QRcode::png(
    'http://www.qq.com',
    false,
    QR_ECLEVEL_L,
    16,
    4
);
```


## 保存二维码到本地文件夹
 存放在temp文件夹下面，并且命名为qq.png

```
<?php

include_once './phpqrcode.php';


header('Content-Type:image/png');



$PNG_TEMP_DIR = dirname(__FILE__) . '/temp/';
$file_name = $PNG_TEMP_DIR . 'qq.png';
QRcode::png(
    'http://www.qq.com',
    $file_name,
    QR_ECLEVEL_L,
    16,
    4
);
```


## 提供二维码的下载

以下方法适用于chrome浏览器

```
<?php

include_once './phpqrcode.php';


try {
    $PNG_TEMP_DIR = dirname(__FILE__) . '/temp/';
    $file_name = $PNG_TEMP_DIR . 'qq.png';
    $download_file_name = 'qq.png';
    QRcode::png(
        'http://www.qq.com',
        $file_name,
        QR_ECLEVEL_L,
        16,
        4
    );
    if (file_exists($file_name)) {
        $file = fopen($file_name, "r");
        Header("Content-type: application/octet-stream");

        Header("Accept-Ranges: bytes");

        Header("Accept-Length: " . filesize($file_name));

        Header("Content-Disposition: attachment; filename=" . $download_file_name);

        // 输出文件内容

        echo fread($file, filesize($file_name));

        fclose($file);
        //下载完成后,删除该图片
        unlink($file_name);
    }

} catch (\Exception $e) {
    echo "无法下载图片\n";
    echo $e->getMessage();
}

```
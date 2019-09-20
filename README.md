# 元数据总结

## JPG

开头: 0xFF 0xD8
结尾: 0xFF 0xD9

数据块分析:

| 数值 | 偏移量      | 长度 | 说明                                       |
| ---- | ----------- | ---- | ------------------------------------------ |
| FF   | +0          | 1    | 开始标识符                                 |
| 任意 | +1          | 1    | 类型,查看规范                              |
| n    | +2 ~ +3     | 2    | 块长度, 包含这两位, 但不包含 FF 和类型长度 |
| 内容 | +4 ~ +(n+2) | n-2  | 内容                                       |

---

已知类型标识符
|数值|说明|额外|
|C0| 宽度高度|+5~+6 高度 +7~+8 宽度|

## PNG

开头固定为:

`89 50 4e 47 0d 0a 1a 0a 00 00 00 0d 49 48 44 52`

宽度在 0x00000010 偏移量处, 0~3 位是宽度 4~7 位是高度

## Webp

开头: 12 字节标识 webp 格式

![20190920150556.png](https://raw.githubusercontent.com/kikt-blog/image/master/img/20190920150556.png)

RIFF(4 字节) + 文件长度(4 字节) + WEBP(4 字节), 文件长度不包含 RIFF 标识头和长度信息, 但包含 WEBP

比如我的图片文件大小为 125,198 字节, 这个文件长度对应的十六进制为 06 E9 01 00 , 这里要注意, 和 png jpg 的长度表示方案不同, 这里是倒序的 0x0001e906 = 125190

---

VP8 chunk: 找到 VP8 的标识 根据内容不同, 表示也不尽相同
往后偏移 `+14 ~ +15` 为宽度(倒序), `16~17`为高度(倒序))
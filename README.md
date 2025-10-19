# custom_font
custom font tips

## 字体构建

1. 使用这个字体作为底：`MapleMonoNL-NF-CN-Regular.ttf`。

2. 打开`FontForge`。然后打开源字体和参考字体：
	1). `MapleMonoNL-NF-CN-Regular.ttf`
	2). `PragmataProR_0828.ttf`

3. 打开字体 -> `Encoding` -> `Reencode` -> `Unicode Full`.
4. 在另外一个字体中找到目标字符。使用菜单`view->Go To`，然后输入比如`0xEB30`就可以到达对应的字符的位置。
5. 在源字体中选中字符 -> `Edit` -> `Copy`。切换到 `Maple Mono` -> 找到对应 `Unicode` 位置 -> `Edit` -> `Paste`。
6. 调整样式（可选），使用 `Element` -> `Transform` -> `Scale` 或 `Metrics` -> `Set Width` 来调整线条粗细、字符宽度。确保视觉风格与 `Maple Mono` 一致。
7. `Element` -> `Font Info` -> `PS Names` 里面修改字体的信息。

| Fontname  | Family Name | Name For Humans    | Weight  |
|-----------|-------------|--------------------|---------|
| VimioMono | Vimio Mono  | Vimio Mono Regular | Regular |

`Fontname` 不能有空格，其他字段可以有空格。
`Font Info` -> `OS/2` -> 修改 `Version` `Vendor ID`.

8. 保存字体，`File` -> `Generate Fonts` -> 保存为新字体，建议命名为 `vimiomono.ttf`。
9. 在`vim`中输入一个自定义的`PUA`区域的字符的方式如下：

```vimscript
:for i in range(0xF57B, 0xF857) | put =nr2char(i) | endfor
```

10. 关于字符方向调节。

```txt
		 ^+
		 |
 -       |           +
 --------+------------> 
		 |
		 | -
```

11. 我当前设计的字符范围。

1). F57B ~ F582 从十字字符到双线交叉字符。
2). F5A0 ~ 开始是单线。
3). F70E ~ 开始是带点。


`X`和`Y`都先缩放`50%`，然后`-200, 400`的位置调整。但是某些字符还是无法对齐，可能需要手动调整。


## 关于unicode字符的私有区域。

| 区域名称                                     | 范围（十六进制）          | 码位数量   | 用途说明               |
|------------------------------------------|-------------------|--------|--------------------|
| Basic Private Use Area (PUA-A)           | U+E000–U+F8FF     | 6,400  | 最常用的私有区，很多字体厂商使用它  |
| Supplementary Private Use Area-A (PUA-B) | U+F0000–U+FFFFD   | 65,534 | 用于更大规模的自定义字符集      |
| Supplementary Private Use Area-B (PUA-C) | U+100000–U+10FFFD | 65,534 | 极少使用，主要用于特殊场景或大型系统 |


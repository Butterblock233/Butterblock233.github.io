+++
title = 'Neovim在插入模式下启用代码诊断'
date = 2024-09-28T23:26:29+08:00
draft = false
tags = ["Neovim"]
author = 'Butterblock233'
+++

Neovim的``lspconfig``有一个让人头大的默认配置：在输入模式下不进行代码诊断，回到正常模式后才刷新诊断。就像这样：![](../images/no%20diagnosis.png)
虽然代码高亮**非常委婉**地指出了这里存在语法错误，但总体的体验还是较差。本文就着手解决这个问题

## 问题分析&解决

Google一圈后发现，这个选项定义于``update_in_insert``中。~~在AI的辅助下~~阅读文档，可以知道需要使用函数``   vim.diagnostic.config()``自定义诊断选项。这时的解决方案就很简单了，只要在配置文件中加入以下代码即可：

```lua
vim.diagnostic.config({update_in_insert = true})
```

大功告成！

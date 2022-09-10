# VSCode 的 Emmet

这是一个语法糖，可以用特殊的格式书写 Emmet，但是因为 vscode 智能提示，这个语法对我有些困扰，下面时解决的办法

[来源](https://stackoverflow.com/questions/61119052/how-do-you-turn-off-emmet-abbreviations-entirely)

1. 第一步在 vscode 设置中搜索 emmet
2. 在 Emmet:Exclude Languages，也就是不应展开 Emmet 缩写的语言数组
3. 点击添加项，添加两个字符——typescriptreact 和 javascriptreact

## 一点想法

这个应该是在前端三大框架前提出的语法糖，用于缓解越来越长和复杂的 html，甚至有可能是在 jQuery 时代前，缩写提供更多的指令或者功能，但是应该没有想到问题的解决不在本身，而是之外的 JavaScript 的工程化时代

原文链接：https://seotoprofit.com/t/topic/4824

一、Cookie 插件下载地址
谷歌浏览器 Cookie 扩展程序（Cookie Editor）下载地址：
:backhand_index_pointing_right: https://chromewebstore.google.com/detail/cookie-editor/hlkenndednhfkekhgcdicdfddnkalmdm?hl=zh-CN

二、为什么导入 Cookie 经常无法使用？
目前市面上购买的 Facebook 账号，常见会附带一段 Cookie 字符串。
很多人会直接把这段字符串复制到 Cookie 扩展程序中导入，但结果往往是：

:cross_mark: 导入成功，但账号无法登录
:cross_mark: 刷新后仍然是未登录状态

原因就在于：

:backhand_index_pointing_right: 大多数提供的 Cookie 字符串，并不是 JSON，而是 Base64 编码后的内容。

如下图所示 :backhand_index_pointing_down:

image
image
1074×1111 432 KB
这种格式 并不能被 Cookie 插件直接识别，所以直接导入是没有任何作用的。

三、正确的使用流程（重点）
正确顺序应该是：
拿到 Cookie 字符串（Base64）
先进行 Base64 解码
得到 完整、可读的 JSON 格式
再使用 Cookie 扩展程序导入
刷新页面 → 登录成功
:warning: Base64 ≠ JSON，必须解码这一步，不能跳过

四、Cookie 解码方式一：在线工具（最快）
下面这些工具 操作方式完全相同：

粘贴 Cookie 内容 → 点击解码 → 得到 JSON

工具 1
https://base64.us/

image
image
2560×1398 181 KB

image
image
2560×1398 291 KB
工具 2
https://tool.tds.qq.com/base64-converter

image
image
1920×1049 324 KB
工具 3
https://toolbox.googleapps.com/apps/encode_decode/?lang=zh-CN

image
image
2560×1398 441 KB
工具 4
https://www.toolhelper.cn/EncodeDecode/Base64

image
image
2560×1398 448 KB
:pushpin: 解码完成后得到的是一个完整的 JSON 数组，这个时候就可以复制 JSON 内容，使用 Cookie 扩展程序导入。

五、Cookie 解码方式二：浏览器控制台（推荐 / 更安全）
:warning: 强烈推荐此方式
因为在线工具存在一定的 Cookie 泄露风险。

操作步骤
:one: 打开浏览器
:two: 按 F12 打开开发者工具
:three: 进入 Console（控制台）
:four: 浏览器会提示“允许粘贴”，输入并确认

image
image
2560×1172 73.8 KB
在控制台粘贴下面代码
:warning: 注意：
把示例中的
WwogIHsKICAgICJkb21haW4iOiAiLmZhY2Vib29rLmNvbSIsCiAgICAiaG9zdE9ubHkiOiBmYWxzZSwK...Cl0=
替换成你自己的 Cookie 内容

const b64 = `WwogIHsKICAgICJkb21haW4iOiAiLmZhY2Vib29rLmNvbSIsCiAgICAiaG9zdE9ubHkiOiBmYWxzZSwK...Cl0=`;
console.log(atob(b64));
:five: 回车执行

执行结果
控制台会直接输出 完整、可读的 JSON 格式 Cookie

image
image
2560×1172 338 KB
复制输出的 JSON → 打开 Cookie 扩展程序 → 导入 → 刷新页面即可。

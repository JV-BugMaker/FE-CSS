# 精通css(二)

## 背景图像

* 默认情况下浏览器水平和垂直地重复显示背景图像
* background-position:left center;--图像元素左边垂直居中
* 使用像素与百分号设置距离都是不一样的，使用百分号是距离左上角与图像的左上角中间段，找图像上距离图像左上角的距离一样的点，进行的
* 不要讲像素单位与百分比这样混合写，会出现异响不到的bug
* border-image--允许指定一个图像作为元素的边框。把图像按照一个简单的百分比规则分成为9部分，浏览器会自动地使用适当的部分作为边框的对应部分。

## 不透明度

* RGBa--是将RGB和alpha结合起来使用:background-color:rgba(0,0,0,0.8)
* IE6中支持PNG透明度,filter:progid:DXImageTransform.Microsoft.AlphaImageLoader(src='/img/xxx.png',sizingMethod='crop')
* text-indent:-5000px; 设置很大的负值来隐藏文本

## 链接

* 层叠样式存在顺序比较重要，:link和:visited样式会覆盖:hover和:active样式。遵循下面的顺序.
	1. a:link
	2. a:visited
	3. a:hover
	4. a:active
* css3中支持:target伪类为目标设置样式
* css3中设置[att^=val],比如a[href^='http://'],如果是http://开头那就是执行下面的样式
* css3中设置[att$=val],比如a[href^='.pdf'],如果是.pdf结尾那就是执行下面的样式
* IE专用开启背景图缓存 filter:expression(document.execCommand("BackgroundImageCache",false,true));

## 表格

* cation:表格标题
* summer:表格标签，类似于img alt属性
* border-collapse 属性设置表格的边框是否被合并为一个单一的边框，还是象在标准的 HTML 中那样分开显示.
	1. separate:默认值。边框会被分开。不会忽略 border-spacing 和 empty-cells 属性。
	2. collapse:如果可能，边框会合并为一个单一的边框。会忽略 border-spacing 和 empty-cells 属性。
	3. inherit:规定应该从父元素继承 border-collapse 属性的值。
*
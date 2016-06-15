#（你需要知道的优化浏览器的方法）
  
  （在过去的几年中,大量的前端性能的责任已经浏览器转换到从开发人员。现在不再是假定“浏览器会更快运行我的代码”,而是“我可以改变代码让浏览器更快。”）
# will-change

[规范，说明](https://www.w3.org/TR/css-will-change/)：
  
  >(在一个会耗费性能的动画执行之前，通知浏览器他们将对这个元素进行什么样的改变，以便让浏览器对这个元素提前进行处理。)
  
  （换言之，你要在这些动画和变换改变之前告诉浏览器我们要做什么事。）
  
  ```css
.element {
  will-change: transform;
}
.element:hover {
  transform: rotateY(180deg);
}
  
  ```
  
  （Sara Soueidan有[一篇更深入的文章](https://dev.opera.com/articles/css-will-change-property/)，我们有[一个年鉴参考](https://css-tricks.com/almanac/properties/w/will-change/)。）
#contain
[规范，说明](https://drafts.csswg.org/css-containment-3/#contain-property):
  
  >（包含属性允许作者表明一个元素及其内容,尽可能独立于其他文档树。这里允许浏览器在呈现页面时恰当的使用contain获得更强的优化，并允许作者相信，他们的页面不会因为缓存路径的改变而发生变化。）
  
  （换言之，换句话说,如果你已经知道某些事情和元素及其后代,你应该告诉浏览器它如何优化这些事情。例如……contain:size;—“这确保包含元素可以无需检查它的后代。”）
###Example(例子)：

```
HTML
  <section class='message'>
    Lol, check out this dog: images.example.com/jsK3jkl
  </section>
  <section class='message'>
    I had a ham sandwich today. #goodtimes
  </section>
  <section class='message'>
    I have political opinions that you need to hear!
  </section>
CSS
  .message {
    contain: strict;
  }
```
  
  (Michael Scharnagl 最近写了[一篇文章](https://justmarkup.com/log/2016/04/css-containment/)：)
  
  >（就像一个内联框架，这个边界建立一个新的布局根,确保DOM改变父文档的子树不会触发回流。）

#Responsive Images（响应式图片）
  
  （也许最明显的“你告诉浏览器”场景是响应图像,特别是大小属性。浏览器将计算每个图像的实际像素密度从指定呈现width和指定的size。它可以选择任何给定的资源，根据用户的屏幕的像素密度,缩放级别,可能还有其他因素,如用户的网络环境。）
Spec(规范，说明)
  
  （这里有一个例子的规范,你给浏览器尽可能使用:）
  
  ```
HTML  
  <img 
  sizes="(max-width: 30em) 100vw, (max-width: 50em) 50vw, calc(33vw - 100px)"
  srcset="swing-200.jpg 200w, swing-400.jpg 400w, swing-800.jpg 800w, swing-1600.jpg 1600w"
   src="swing-400.jpg" 
  alt="Kettlebell Swing"
>
  ```
  
  *（如果浏览器窗口小于30 em,我会显示图像宽100vw。）
  
  *（如果浏览器窗口在30 em和50 em之间,我会显示图像宽50vw。）
  
  *（否则(如果它更大),我将显示图像宽为(33vw - 100 px)。）
  
  （然后需要匹配你实际做的CSS。希望它是相当准确的,才能实现浏览器屏大小与图片相匹配。）
#A Brave New World（一个美好的新世界）
  
  （我提到这些事情不是因为我认为你需要立即开始使用所有这些。如果可以，把焦点更多的放在浏览器的前端性能特征上。）
  
  （我认为浏览器厂商和规范作者会说:“你想要的性能。我们只有这么多。有些事情我们不知道,但你知道。如果你告诉我们我们可以做得更好。”）
  
  （你说呢？）


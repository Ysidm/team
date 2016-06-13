# Ways You Need To Tell The Browser How To Optimize（你需要知道的优化浏览器的方法）

In the past few years, there has been a number of front end features in which the performance onus has shifted from browser to developer. Rather than the presumed "browsers will get faster at running my code", there is a little more "I need to change the way I code for browsers to get faster."（在过去的几年里，）
# will-change
Spec(规范，说明)
Blockquote(引用):
>allows an author to inform the UA ahead of time of what kinds of changes they are likely to make to an element. This allows the UA to >optimize how they handle the element ahead of time, performing potentially-expensive work preparing for an animation before the >animation actually begins.（允许作者提前告知浏览器的默认样式，那他们可能会做出一个元素。它允许对浏览器默认样式的优化如何提前处理因素，在动画实际开始之前，为准备动画所执行的潜在昂贵的工作。）
Blockquote.
In other words, in addition to using animations and transforms, tell the browser what you are going to change within those animations and transforms.
（换言之，除了使用动画和变换，你要在动画和变换这些变化前告诉浏览器）
.element { will-change: transform; } 
.element:hover { transform: rotateY(180deg); }
Sara Soueidan has a more in-depth article and we have an almanac reference.
（Sara Soueidan有一篇更深入的文章，我们有一个年鉴参考。）
#contain
Spec(规范，说明)
Blockquote(引用):
>The contain property allows an author to indicate that an element and its contents are, as much as possible, independent of the rest >of the document tree. This allows user agents to utilize much stronger optimizations when rendering a page using contain properly, >and allows authors to be confident that their page won’t accidentally fall into a slow code path due to an innocuous change.（包含属性允许作者表明一个元素及其内容,尽可能独立于其他文档树。这里允许浏览器在呈现页面时恰当的使用contain获得更强的优化，并允许作者相信，他们的页面不会因为缓存路径的改变而发生变化。）
Blockquote
In other words, if you know certain things about an element and its descendants, you should tell the browser so it can optimize around those things. For example... contain: size; - "This ensures that the containing element can be laid out without needing to examine its descendants."
（换言之，换句话说,如果你知道某些事情和元素及其后代,你应该告诉浏览器它可以优化这些事情。例如……contain:size;—“这确保包含元素可以无需检查它的后代。”）
Example(例子):
html
><section class='message'>
> Lol, check out this dog: images.example.com/jsK3jkl</section><section class='message'>
>  I had a ham sandwich today. #goodtimes</section><section class='message'>
>   I have political opinions that you need to hear!</section>
CSS
>.message {
>  contain: strict;}
Michael Scharnagl recently wrote a post on this:(Michael Scharnagl 最近写了一篇文章：)
Much like an iframe, this boundary establishes a new layout root, ensuring that DOM changes in the sub-tree never trigger reflows in the parent document.
（就像一个内联框架，这个边界建立一个新的布局根,确保DOM改变父文档的子树不会触发回流。）
#Responsive Images（响应式图片）
Perhaps the most visible of these "you tell the browser what's up" scenarios is responsive images, and particularly the sizes attribute.
（也许最明显的“你告诉浏览器”场景是响应图像,特别是大小属性。浏览器将计算每个图像的实际像素密度从指定呈现宽描述符和指定的大小的大小属性。它可以选择任何给定的资源根据用户的屏幕的像素密度,缩放级别,可能还有其他因素,如用户的网络环境。）
Spec(规范，说明)
Blockquote(引用):
>The user agent will calculate the effective pixel density of each image from the specified w descriptors and the specified rendered >size in the sizes attribute. It can then choose any of the given resources depending on the user’s screen’s pixel density, zoom >level, and possibly other factors such as the user’s network conditions.（浏览器将计算每个图像的有效像素密度从指定呈现宽描述符和指定呈现的尺寸属性。它可以选择任何给定的资源根据用户的屏幕的像素密度,缩放级别,可能还有其他因素,如用户的网络环境。）
Here's an example from the spec, where you're giving the browser as much as you can to work with:
（这里有一个例子的规范,你给浏览器尽可能使用:）
><img sizes="(max-width: 30em) 100vw, (max-width: 50em) 50vw, calc(33vw - 100px)" srcset="swing-200.jpg 200w, swing-400.jpg 400w, swing-800.jpg 800w, swing-1600.jpg 1600w" src="swing-400.jpg" alt="Kettlebell Swing" >
Which says...（）
>If the browser window is narrower than 30em, I'll be displaying the image at 100vw wide.
（如果浏览器窗口小于30 em,我会显示图像宽100vw。）
>If the browser window is between 30em and 50em, I'll be displaying the image at 50vw wide.
（如果浏览器窗口在30 em和50 em之间,我会显示图像宽50vw。）
>Otherwise (if it's even bigger), I'll be displaying the image at calc(33vw - 100px) wide.
（否则(如果它更大),我将显示图像宽为(33vw - 100 px)。）
Which then needs to match up with what you actually do in the CSS. Hopefully it's fairly accurate, so the browser optimizations match up with reality.
（然后需要匹配你实际做的CSS。希望它是相当准确的,所以浏览器优化与现实相匹配。）
#A Brave New World（一个美好的新世界）
I mention these things not because I think you need to run out and start using all this immediately. More to spotlight the (if I may) trend, in front end performance-related features in which the browsers ask more of authors.（我提到这些事情不是因为我认为你需要立即跑出去开始使用所有这些。更多的焦点（如果可以）趋势，在前端性能特征的浏览器问更多的作者。）
I think the browser vendors and spec authors would say: "You want performance. There is only so much we can do. There are certain things we can't know, but you do know. We'll do our best without them, but if you tell us about them we can do much more."（我认为浏览器厂商和规范作者会说:“你想要的性能。我们只有这么多。有些事情我们不知道,但你知道。我们将尽一切没有它们,但是如果你告诉我们我们可以做得更多。”）
What say you?（你说呢？）


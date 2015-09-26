---
layout: post
title: 原生js与jq网页遮罩层
---


![mahua](mahua-logo.jpg)

####谈谈网页遮罩层
很多时候弹出对话框或者其他项目的时候都用到遮罩层。

总结如下：

实现原理 

个人理解实现原理如下： 

* 实际上弹出层、遮罩层和原页面显示分别为三个不同的div 。

* 弹出层的层级在遮罩层之上，遮罩层的层级在原页面显示之上。 

* 遮罩层有改变透明度效果 。

* 遮罩层没有实际意义，则无需在html部分就写上，当然写上同样可以实现。 

原生js实现：

        window.onload = function() {

            var Odiv = document.createElement('div'),

                docH = document.body.offsetHeight;

            Odiv.setAttribute('id', 'mask');

            Odiv.style.background = "#000";

            Odiv.style.width = "100%";

            Odiv.style.height = docH + "px";

            Odiv.style.position = "absolute";

            Odiv.style.top = "0";

            Odiv.style.left = "0";

            Odiv.style.zIndex = "500";

            Odiv.style.opacity = "0.3";

            Odiv.style.filter = "Alpha(opacity=30)";

            document.body.style.overflow = "hidden"; //禁止屏幕滚动

            document.body.appendChild(Odiv);

            setTimeout(function() {

                Odiv.style.display = 'none';

            }, 3000);

        }



改造成jq形式：

                $(function(){

                    var oDiv = $('<div>',{

                                 "id":"mask"

                                 }),

                        docH = $(document).height();

                    oDiv.css({

                        'position':'absolute',

                        'background-color':'red',

                        'left':0,

                        'top':0,

                        'width':'100%',

                        'opacity':.5,

                        'height':docH,

                        'z-index': 5000

                        

                    })

                    oDiv.appendTo('body');

                })

这里用z-index来区分层级，opacity和filter：alpha（opacity=）添加透明度，document.createElement("div")和document.body.appendChild()把这个div插入到body头部。原理就这样简单，当然也可以封装成方法方便每次使用。

明白了原理直接在body下面加htm其实也能实效遮罩，具体看怎么方便怎么玩咯～

   <div class="mask-cj" style="display:none; position:absolute; width:100%; height:100%; top:0; left:0; z-index:888;background:rgba(0,0,0,0.5);"> </div>

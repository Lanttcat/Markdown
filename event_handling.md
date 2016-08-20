# web开发小记3：事假处理函数

因为IE浏览器和其他浏览器有不同的处理事件的函数，所以需要拿出一个跨浏览器的解决方案。
```JavaScript
<script>
           // 跨浏览器事件对象
           //原因：DOM和IE中的event对象不同，但是有一些相似性。所以可以拿出一个跨浏览器的解决方案
           var EventUtil = {
               addHander:function(element,type,handler){
                   if(element.addEventListener){
                       //DOM处理添加监听事件
                       element.addEventListener(type, handler, false);
                   }else if(element.attachEvent){
                       //IE处理添加监听事件
                       element.attachEvent("on" + type, handler);
                   }else{
                       element["on" + type] = handler;
                   }
               },
               removeHander:function(element, type, handler){
                   if (element.removeHander) {
                       element.removeHander(type, handler, false);
                   }else if (element.detachEvent) {
                       element.detachEvent("on" + type, handler)
                   }else {
                       element["on" + type] = null;
                   }
               },
               getEvent:function(event){
                   return event?event:window.event;
               },
               getTarget:function(event) {
                   return event.target || event.srcElement;
               }
           }
       </script>
```

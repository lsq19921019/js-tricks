macrotasks: setTimeout ，setInterval， setImmediate，requestAnimationFrame,I/O ，UI渲染

microtasks: Promise， process.nextTick， Object.observe， MutationObserver

当一个程序有：setTimeout， setInterval ，setImmediate， I/O， UI渲染，Promise ，process.nextTick， Object.observe， MutationObserver的时候：

1.先执行 macrotasks：I/O -》 UI渲染-》requestAnimationFrame

2.再执行 microtasks ：process.nextTick -》 Promise -》MutationObserver ->Object.observe

3.再把setTimeout setInterval setImmediate【三个货不讨喜】 塞入一个新的macrotasks，依次：setTimeout ，setInterval --》setImmediate

<img src="https://pic2.zhimg.com/50/v2-a99898e192654136eabcc934aa29f725_720w.jpg?source=1940ef5c" data-caption="" data-rawwidth="720" data-rawheight="343" class="origin_image zh-lightbox-thumb" width="720" data-original="https://pic2.zhimg.com/v2-a99898e192654136eabcc934aa29f725_r.jpg?source=1940ef5c"/>

setImmediate(function(){
    console.log(1);
},0);
setTimeout(function(){
    console.log(2);
},0);   
new Promise(function(resolve){
    console.log(3);
    resolve();
    console.log(4);
}).then(function(){
    console.log(5);
});
console.log(6);
process.nextTick(function(){
    console.log(7);
});
console.log(8);
结果是：3 4 6 8 7 5 2 1

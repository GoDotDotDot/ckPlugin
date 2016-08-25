you just need use flowing code to init checkbox.
```html
<div id="ckPlugin"></div>
```
```js
var chk = new ckCheck(7,10,[1,2,3,4,5,6,7,8,9,10])
chk.start();
/*
*7 is mask code,just for initializing checkbox 
*10 is count of your checkbox
*[1,2,3.....] is text for display in you checkbox 
*/
```

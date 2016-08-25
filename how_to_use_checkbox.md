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
demo
```html
<!DOCTYPE html PUBLIC "-//W3C//Dth XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/Dth/xhtml1-transitional.dth">
<html xmlns="http://www.w3.org/1999/xhtml">
<meta charset="UTF-8">
<head>
</head>
<body>
	<div id="ckPlugin"></div>
	result：<label id="ck-Res">0</label>
	<button class="ck-selectAll">全选(All)</button>
	<button class="ck-inverse">反选(None)</button>
	<button class="ck-default">默认值(Default)</button>
	<hr />	
</body>
</html>
<script>

	function ckCheck (mask,text) {
		this.mask = mask;//mask code for default value 掩码值，用于默认值
		this.temp = mask;// temp for cache and store which checkbox is selected 缓存值用于操作，并且存储哪一个checkbox被选中。
		this.nodes = [];//store node
		this.num = text.length;//nodes count
		this.text = text//per node text
	}
	ckCheck.prototype={
		start:function () {
			this.addElement(this.num,this.text);
			this.nodes = this.selectorAll('.ckPlugin');
			this.default();
			this.addEvtLisener();
		},
		addElement:function (num,text) {
			var html =  '';
			for(var i = 0;i < num;i++){
				html+=  ('<input type="checkbox" value= "'+Math.pow(2,i)+'" class= "ckPlugin" >'+text[i]);
			}
			this.selector("#ckPlugin").innerHTML=html
		}
		,
		showCheckedNums:function(argument){
			//just for display  仅仅用于展示
			document.getElementById("ck-Res").innerHTML= this.temp;
		},
		default:function (argument) {
            //back to initial value
			for(var j = 0;j<this.nodes.length ;j++){
				//init checkbox
				this.nodes[j].checked = this.nodes[j].value & this.mask ;//1
				this.temp = this.mask;
			};
			this.showCheckedNums();
		},
		addEvtLisener:function(){
            var self = this;
			for(var i = 0; i < this.nodes.length; i++){
				self.nodes[i].addEventListener('click', function (e) {
					e.target.checked ? self.temp|=e.target.value:self.temp^=e.target.value;
					self.showCheckedNums();
				})
			};
			var sAll = this.selector('.ck-selectAll');
			var inv = this.selector('.ck-inverse');
			var def = this.selector('.ck-default');
		
			sAll ? sAll.addEventListener('click', function () {
			 		 self.selectAll(self);
			}):console.log('全选功能没有启用！如需启用，请添加类名为："ck-selectAll"')
			
			inv ? inv.addEventListener('click', function () {
				  self.inverse(self);
			}):console.log('反选功能没有启用!如需启用，请添加类名为："ck-inverse"');
			def ? def.addEventListener('click', function () {
				  self.default(self);
			}):console.log('默认功能没有启用！如需启用，请添加类名为："ck-default"');
		},
		selectorAll:function (selector) {
			if (document.querySelectorAll(selector)) {
				return document.querySelectorAll(selector)
			}
			else {
				console.log('没有找到选择器')
			}
		},
		selector:function (selector) {
			if(document.querySelector(selector)){
				return document.querySelector(selector) 
			}
			else {
				console.log('没有找到选择器')
			}
		},
		selectAll:function (self) {
			for(var i = 0; i <  self.nodes.length; i++){
				self.nodes[i].checked ? null: self.nodes[i].checked = self.temp|=self.nodes[i].value;
			}
			self.showCheckedNums();
		},
		inverse:function (self) {			
			for(var i = 0; i <  self.nodes.length; i++){
				self.nodes[i].checked = (self.temp ^=self.nodes[i].value) & self.nodes[i].value
			}			
			self.showCheckedNums();
		}	
	}
	

	var obj = new ckCheck(7,[1,2,3,4,5,6,7,8,9,10])
	obj.start();
</script>
```

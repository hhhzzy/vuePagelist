<template>
	<div class="box">
		<h3>简洁的做法，比较难理解的分页</h3>
		<nav aria-label="Page navigation">
		  <ul class="pagination" >
		    <li >
		      <a href="#" aria-label="Previous" v-show=" current != 1 " @click="current-- && btnClick(current)" >
		        <span aria-hidden="true">上一页</span>
		      </a>
		    </li>
		    <!-- <li><a href="#">1</a></li>
		    <li><a href="#">2</a></li>
		    <li><a href="#">3</a></li>
		    <li><a href="#">4</a></li>
		    <li><a href="#">5</a></li> -->
		    <li  v-for=" pageNum in pages " v-on:click="btnClick(pageNum)" :class="{'active':current == pageNum}"  :key="current" >
		    	<a href="#" >{{pageNum}}</a>
		    </li>
		    <li>
		      <a href="#" aria-label="Next" v-show=" current != allPage " @click="current++ && btnClick(current)">
		        <span aria-hidden="true">下一页</span>
		      </a>
		    </li>
		    <li>
		      <a href="">共多少页：{{allPage}}</a>
		    </li>
		  </ul>
		</nav>
	</div>
</template>
<script>
	export default{
		data(){
			return {
				current:1, //当前显示的页码数
				showItem:5, //要显示的页码数
				allPage:13   //总的页码数
			}
		},
		computed:{
			pages(){
				var pages= [];//定义一个数组，来装要显示的页码
				//如果当前显示的页码数（current）小于要的显示页码数（showItem）
				if(this.current < this.showItem){
					var i = Math.max(this.current,this.showItem);
					while(i){
						pages.unshift(i--);
					}
				}else{
					var middle = this.current - Math.floor(this.showItem / 2 ),//从哪里开始
                           i = this.showItem;
                    //判断总的页数显示完成后，就停止增加页码
                    if( middle >  (this.allPage - this.showItem)  ){
                       middle = (this.allPage - this.showItem) + 1
                    }
                    while(i--){
                       pages.push( middle++ );
                    }

				}
				return pages;
			}
		},
		methods:{
			btnClick(ind){
				if(ind == this.current) return;
				this.current = ind;
			}
		}
	}
</script>
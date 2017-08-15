<template>
	<div id="pageList">
		<h3>通俗的做法，比较好理解的分页</h3>
		<nav aria-label="Page navigation">
		  <ul class="pagination" >
		    <li >
		      <a href="#" aria-label="Previous" @click="current-- && btnClick(current)" v-show=" current != 1 " >
		        <span aria-hidden="true">上一页</span>
		      </a>
		    </li>
		    <!-- <li><a href="#">1</a></li>
		    <li><a href="#">2</a></li>
		    <li><a href="#">3</a></li>
		    <li><a href="#">4</a></li>
		    <li><a href="#">5</a></li> -->
		    <li  v-for=" pageNum in pages " v-on:click="btnClick(pageNum)" :class="{'active':current == pageNum}"  >
		    	<a href="#" >{{pageNum}}</a>
		    </li>
		    <li>
		      <a href="#" aria-label="Next" @click=" current++ && btnClick(current) " v-show = " current != allpage ">
		        <span aria-hidden="true">下一页</span>
		      </a>
		    </li>
		    <li>
		      <a href="">共多少页：{{allpage}}</a>
		    </li>
		  </ul>
		</nav>
	</div> 
</template>
<script>
		export default{
			data(){
				return {
					current:1,   //当前显示的页码数
		            showItem:7,  //显示出来的条数
		            allpage:13   //总的页码数
				}
			},
			 computed:{
		         pages(){
		         	var pages = [];//装入要显示的页码数
		         	//当前显示的页码数（current）小于显示的页数（showItem）,pages里面就装大于（current）显示的页码数
		         	if(this.current < this.showItem){
		         		var i = Math.max(this.current,this.showItem);
		         		while(i){
		         			pages.unshift(i--);
		         		}
		         	}else{
		         		var i;
		         		//只有当前显示的页数小于等于总页数是才会出现
		         		if(this.current <= this.allpage-Math.floor(this.showItem/2)){
		         			i = this.current + Math.floor(this.showItem/2);  //能够显示出来页数的最大值
							
		         		}else{
							i = this.allpage;  //能够显示出来页数的最大值
		         		}
		         		//从最大值开始往下面放数字，一直到显示的个数
		         		for(var j = 0;j < this.showItem; j ++){
		         			pages.unshift(i--);
		         		}
		         		
		         	}
		         	return pages;
		         }
		      },
			methods:{
				btnClick(ind){
					// alert(ind);
					if(ind == this.current){
						return ;
					}else{
						this.current = ind;
					}
				}
			}
		}
</script>
<style scoped>
	.active{background: #0E90D2;color: #fff;}
</style>
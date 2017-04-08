# vue2.0
学习vue

1.首先 是table表格的数据的表现的
2.model的弹出的
3.model中的值传递的
4.增删改查的实现，难点在编辑的功能


详解编辑得实现的
model的几个步骤
1. <modal-update v-if="showModalUpdate" @close="showModalUpdate = false"  @update="update()"  :my-tag-update-r="selectTagUpdate"></modal-update>官方文档中讲解的
2.要有触发model出来的按钮 <button class="btn  btn-primary"  @click="openTagModalUpdate(person, index)">编辑</button>

3.data：{
      showModalUpdate: false,
      selectTagUpdate:null,
}

4.css代码
从页面到model的传值步骤

1.:my-tag-update-r="selectTagUpdate"  传值

2. components:{
      'modal-update':{
           props: ['myTagUpdateR'],           
           template: '#modal-template-update'
       }
  }
  
当我们修改model中值会主动修改视图的值所以应该先把值拷贝一份的
//编辑--打开model
     openTagModalUpdate:function(tag,index){
         //console.info(tag)
         //打开模态框的要求
         this.showModalUpdate = true;
         let cache = Object.assign({},tag)    //拷贝代码的
         this.$set(this.cache,'person',cache);    //吧修改的新的值重新刷新
         this.$set(this.cache,'index',index);
         this.selectTagUpdate = cache;
     },

     //编辑model---提交
      update:function(){
         console.info(111)
         let index = this.cache.index;      //刷新页面的  同步数据
         let person = this.cache.person;
         this.$set(this.people,index,person);
         this.showModalUpdate = false;
      }

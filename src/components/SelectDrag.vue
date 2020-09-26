<template>
<div class="ul-container">
  <div class="list">
    <ul ref="lists">
      <li v-for="item in virtualList" :key="item.id" draggable="true" @dragstart.stop="dragItem">
        <span>{{item.text}}</span>
        <span>{{item.department}}</span>
      </li>
    </ul>
    <div id="moveSelected"></div>
  </div>
</div>
</template>

<script>
export default {
  name: 'HelloWorld',
  props: {
    
  },
  data() {
    return {
      isSelected:false,
      virtualList: [
        {id: 1, text: '林嘉恒', department: '交互技术部'},
        {id: 2, text: '林嘉恒', department: '交互技术部'},
        {id: 3, text: '林嘉恒', department: '交互技术部'},
        {id: 4, text: '林嘉恒', department: '交互技术部'},
        {id: 5, text: '林嘉恒', department: '交互技术部'},
        {id: 6, text: '林嘉恒', department: '交互技术部'},
        {id: 7, text: '林嘉恒', department: '交互技术部'},
        {id: 8, text: '林嘉恒', department: '交互技术部'},
        {id: 9, text: '林嘉恒', department: '交互技术部'},
        {id: 10, text: '林嘉恒', department: '交互技术部'}
      ],
      moveSelected: null,
      flag: false,
      oldLeft: 0,
      oldTop: 0,
      selectedList: [],
    }
  },
  watch: {
    // isSelected(val) {
    //   if(!val) {
    //     let lists = Array.from(this.$refs.lists.children)
    //     for(let i in lists) {
    //       lists[i].classList.remove('selected')
    //     }
    //   }
    // }
  },
  methods: {
    dragItem(ev) {
      console.log(ev)
    },
      findSelected(){
            let blockList=this.$refs.lists.children
            console.log(this.$refs.lists.children)
            for(let i=0;i<blockList.length;i++){
              console.log(222)
                //计算每个块的定位信息
                let left=blockList[i].offsetLeft;
                let right=blockList[i].offsetWidth+left;
                let top=blockList[i].offsetTop;
                let bottom=blockList[i].offsetHeight+top;
                //判断每个块是否被遮罩盖住（即选中）
                let leftFlag=this.moveSelected.style.left.split('px')[0]<=left && left<=this.moveSelected.style.right.split('px')[0];
                let rightFlag=this.moveSelected.style.left.split('px')[0]<=right && right<=this.moveSelected.style.right.split('px')[0];
                let topFlag=this.moveSelected.style.top.split('px')[0]<=top && top<=this.moveSelected.style.bottom.split('px')[0];
                let bottomFlag=this.moveSelected.style.top.split('px')[0]<=bottom && bottom<=this.moveSelected.style.bottom.split('px')[0];
                if((leftFlag || rightFlag) && (topFlag || bottomFlag)){
                    this.selectedList.push(blockList[i]);
                   blockList[i].classList.add('selected');
                   this.isSelected = true
                    console.log(blockList[i])
                }
            }
            console.log(this.selectedList);
        },
        clearDragData(){
            this.moveSelected.style.width=0;
            this.moveSelected.style.height=0;
            this.moveSelected.style.top=0;
            this.moveSelected.style.left=0;
            this.moveSelected.style.bottom=0;
            this.moveSelected.style.right=0;
        }
  },
  mounted() {
    this.moveSelected = document.getElementById('moveSelected')
    let list = document.getElementsByClassName('list')[0]
    list.addEventListener('mousedown', ev => {
      // console.log(ev)
      if(this.isSelected) {
        this.isSelected = false
      }
      this.flag = true
      this.moveSelected.style.top = ev.pageY + 'px'
      this.moveSelected.style.left = ev.pageX + 'px'
      this.oldLeft = ev.pageX
      this.oldTop = ev.pageY
      ev.preventDefault()
      ev.stopPropagation()
    })
    list.addEventListener('mousemove', ev => {
      if(!this.flag) return;//只有开启了拖拽，才进行mouseover操作
      // console.log(ev)
      if(ev.pageX < this.oldLeft){//向左拖
          this.moveSelected.style.left=ev.pageX+'px';
          this.moveSelected.style.width=(this.oldLeft-ev.pageX)+'px';
      }else{
          this.moveSelected.style.width=(ev.pageX-this.oldLeft)+'px';
      }
      if(ev.pageY<this.oldTop){//向上
          this.moveSelected.style.top=ev.pageY+'px';
          this.moveSelected.style.height=(this.oldTop-ev.pageY)+'px';
      }else{
          this.moveSelected.style.height=(ev.pageY-this.oldTop)+'px';
      }
      ev.preventDefault();  // 阻止默认行为
      ev.stopPropagation(); // 阻止事件冒泡
    })
    list.addEventListener('mouseup', ev => {
      this.moveSelected.style.bottom=Number(this.moveSelected.style.top.split('px')[0])+Number(this.moveSelected.style.height.split('px')[0]) + 'px';
      this.moveSelected.style.right=Number(this.moveSelected.style.left.split('px')[0])+Number(this.moveSelected.style.width.split('px')[0])+'px';
      this.findSelected();
      this.flag=false;
      this.clearDragData();
      ev.preventDefault();  // 阻止默认行为
      ev.stopPropagation(); // 阻止事件冒泡
    })
    list.addEventListener('mouseleave', ev => {
      console.log('离开元素')
      this.flag = false
      this.moveSelected.style.width = 0
      this.moveSelected.style.height = 0
      this.moveSelected.style.top = 0
      this.moveSelected.style.left = 0
      ev.preventDefault()
      ev.stopPropagation()
    })
  }
}
</script>
<style >
.ul-container {
  width: 100vw;
  padding-top: 40px;
}
.ul-container .list {
  position: relative;
  width: 1800px;
  height: calc(100vh - 20px);
  margin: 0 auto;
  border: 1px solid #333;
}
.ul-container .list ul {
  display: flex;
  flex-wrap: wrap;
}
.ul-container .list #moveSelected {
  position: absolute;
  top: 0;
  left: 0;
  background-color: blue;
  opacity:0.3;
  border:1px dashed #d9d9d9;
}
.ul-container .list ul li {
  list-style: none;
  width: 240px;
  height: 240px;
  background: blanchedalmond;
  margin-right: 30px;
  margin-bottom: 20px;
  cursor: pointer;
  /* display: flex; */
}
.ul-container .list ul .selected {
  background-color: pink;
}
</style>

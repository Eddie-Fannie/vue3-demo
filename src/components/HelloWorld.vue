<template>
  <!-- <h1>{{ msg }}</h1>
  <button @click="count++">count is: {{ count }}</button>
  <p>Edit <code>components/HelloWorld.vue</code> to test hot module replacement.</p> -->
  <div class="virtual-list">
    <div class="virtual-list__container">
      <ul @mousewheel="wheelContainer" ref="wheelUl" id="wheel_container">
        <li v-for="(item,index) in virtualList" :key="item.id">
          <span>{{item.id}}</span>
          <span>{{item.text}}</span>
          <span>{{item.department}}</span>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },
  data() {
    return {
      count: 0,
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
        {id: 10, text: '林嘉恒', department: '交互技术部'},
        {id: 11, text: '林嘉恒', department: '交互技术部'},
        {id: 12, text: '林嘉恒', department: '交互技术部'},
        {id: 13, text: '林嘉恒', department: '交互技术部'},
        {id: 14, text: '林嘉恒', department: '交互技术部'},
        {id: 15, text: '林嘉恒', department: '交互技术部'},
        {id: 16, text: '林嘉恒', department: '交互技术部'},
        {id: 17, text: '林嘉恒', department: '交互技术部'},
        {id: 18, text: '林嘉恒', department: '交互技术部'},
        {id: 19, text: '林嘉恒', department: '交互技术部'},
        {id: 20, text: '林嘉恒', department: '交互技术部'},
        {id: 21, text: '林嘉恒', department: '交互技术部'}
      ]
    }
  },
  watch: {
    count(newVal) {
      console.log(newVal)
    }
  },
  methods: {
    wheelContainer(ev) {
      console.log(ev)
      console.log(this.$refs)
      // this.$refs.wheelUl.style.transform = `translateY(-${30}px)`
      if(ev.wheelDelta < 0) {
        if(this.count === this.virtualList.length-1) return;
        this.count++
      } else {
        if(this.count === 0) return
        this.count--
      }
      this.$refs.wheelUl.style.transform = `translateX(0px)`
      this.$refs.wheelUl.style.transform = `translateY(-${30*this.count}px)`
    }
  }
}
</script>
<style >
.virtual-list {
  height: 400px;
}
.virtual-list .virtual-list__container {
  margin: 0 auto;
  width: 400px;
  height: 400px;
  max-height: 500px;
  overflow: hidden;
  position: relative;
  background-color: beige;
}
.virtual-list .virtual-list__container ul {
  width: 400px;
  border: 1px solid #333;
  position: absolute;
  top: 0;
  left: 50%;
  transform: translate(-50%,0);
}
.virtual-list .virtual-list__container ul li {
  /* width: 100%; */
  height: 30px;
  display: flex;
  justify-content: space-between;
  background-color: #86889e;
}
.virtual-list .virtual-list__container ul li span {
  color: #333;
  font-size: 18px;
}
</style>

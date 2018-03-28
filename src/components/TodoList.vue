<template>
  <div>
    <wxc-minibar  title="标题"
                  background-color="#009ff0"
                  text-color="#FFFFFF"
                  leftButton=""
                  right-text="+"
                  @wxcMinibarRightButtonClicked="minibarRightButtonClick">
      <input  slot="middle"
              class="input"
              @focus="onFocus"
              @input="onInput"
              @change="onChange"
              placeholder="Add Todo"/>
    </wxc-minibar>
    <list @loadmore="fetch" loadmoreoffset="0">
      <cell v-for="(item, i) in todoLists" :key="i" @click="click(item, i)">
        <div class="panel">
          <text class="text">{{item}}</text>
        </div>
      </cell>
    </list>
  </div>
</template>

<style scoped>
  .input {
    font-size: 26px;
    height: 60px;
    flex: 1;
    border-radius: 20px;
    background-color: white;
  }
  .panel {
    /* width: 600px; */
    flex: 1;
    /* height: 250px; */
    margin-left: 30px;
    margin-right: 30px;
    margin-top: 20px;
    padding-top: 10px;
    padding-bottom: 10px;
    flex-direction: column;
    justify-content: center;
    border-width: 2px;
    border-style: solid;
    border-color: rgb(162, 217, 192);
    background-color: rgba(162, 217, 192, 0.2);
  }
  .text {
    font-size: 30px;
    text-align: center;
    color: #41B883;
  }
</style>

<script>
import { WxcMinibar } from 'weex-ui'
const modal = weex.requireModule('modal')
const LOADMORE_COUNT = 4

export default {
  components: { WxcMinibar },
  data () {
    return {
      txtInput: '',
      todoLists: [1, 2, 3, 4, 5],
      finishedLists: []
    }
  },
  methods: {
    fetch (event) {
      // modal.toast({ message: 'loadmore', duration: 1 })
      setTimeout(() => {
        // const length = this.todoLists.length
        // for (let i = length; i < length + LOADMORE_COUNT; ++i) {
          // this.todoLists.push(i + 1)
        // }                                                                                          
      }, 800)
    },
    click (item, i) {
      modal.toast({ message: 'Good', duration: 1 })
      this.finishedLists.push(item)
      this.todoLists.splice(i, 1)
    },
    minibarRightButtonClick () {
      this.todoLists.push(this.txtInput)
      modal.toast({ 'message': '添加成功!', 'duration': 1 })
    },
    onInput (event) {
      this.txtInput = event.value
      console.log('oninput', event.value)
    },
    onChange (event) {
      this.txtInput = event.value
      console.log('onchange', event.value)
    },
    onFocus (event) {
      console.log('onfocus')
    }
  }
}
</script>

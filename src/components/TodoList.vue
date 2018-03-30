<template>
  <div>
    <wxc-minibar  title="标题"
                  background-color="#009ff0"
                  text-color="#FFFFFF"
                  leftButton="">
      <input  slot="middle"
              class="input"
              @focus="onFocus"
              @input="onInput"
              @change="onChange"
              placeholder="Add Todo"/>
      <text slot="right"
            class="add"
            @click="minibarRightButtonClick">+</text>
    </wxc-minibar>
    <text class="title">正在进行</text>
    <list @loadmore="fetch" loadmoreoffset="0">
      <cell v-for="(item, i) in todoList" :key="i" @click="cellClick(item, i)">
        <div class="panel">
          <div @click="itemCheck(item, i)" :class="['checkbox', { 'checkboxChecked' : item.checked }]"></div>
          <text class="text">{{item.title}}</text>
        </div>
      </cell>
    </list>
    <text class="title">已经完成</text>
    <list @loadmore="fetch" loadmoreoffset="0">
      <cell v-for="(item, i) in finishedList" :key="i">
        <div class="panel">
          <div @click="itemCheck(item, i)" :class="['checkbox', { 'checkboxChecked' : item.checked }]"></div>
          <text class="text">{{item.title}}</text>
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
  .add {
    font-size: 60px;
  }
  .checkbox {
    width: 42px;
    height: 42px;
    background: chartreuse;
  }
  .checkboxChecked {
    background: burlywood;
  }
  .title {
    font-size: 48px;
    padding-left: 20px;
    padding-top: 20px;
    font-weight: bold;
  }
  .panel {
    flex: 1;
    margin-left: 30px;
    margin-right: 30px;
    margin-top: 20px;
    padding-top: 10px;
    padding-bottom: 10px;
    flex-direction: row;
    justify-content: center;
    border-width: 2px;
    border-style: solid;
    border-color: rgb(162, 217, 192);
  }
  .text {
    flex: 1;
    font-size: 30px;
    text-align: center;
    align-self: center;
    color: #41B883;
  }
</style>

<script>
import { WxcMinibar, WxcCheckbox } from 'weex-ui'
const modal = weex.requireModule('modal')

export default {
  components: { WxcMinibar, WxcCheckbox },
  data () {
    return {
      txtInput: '',
      todoList: [
        {title:1, checked: false},
        {title:2, checked: false},
        {title:3, checked: false},
        {title:4, checked: false},
        {title:5, checked: false},
      ],
      finishedList: []
    }
  },
  methods: {
    fetch (event) {
      setTimeout(() => {
      }, 800)
    },
    cellClick (item, i) {
      // modal.toast({ message: 'Good', duration: 1 })
      // this.finishedList.push(item)
      // this.todoList.splice(i, 1)
    },
    itemCheck (item, i) {
        modal.toast({ message: 'Good', duration: 1 })
        this.todoList[i].checked = true
        this.finishedList.push(item)
        this.todoList.splice(i, 1)
    },
    minibarRightButtonClick () {
      if (this.txtInput) {
        this.todoList.push( {title: this.txtInput, checked: false })
        modal.toast({ 'message': '添加成功!', 'duration': 1 })
        this.txtInput = ""
      }
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

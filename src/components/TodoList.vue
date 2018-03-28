<template>
  <div>
    <wxc-minibar style="" 
                  title="标题"
                  background-color="#009ff0"
                  text-color="#FFFFFF"
                  leftButton=""
                  right-text="Add"
                  @wxcMinibarLeftButtonClicked="minibarLeftButtonClick"
                  @wxcMinibarRightButtonClicked="minibarRightButtonClick">
    </wxc-minibar>
    <list @loadmore="fetch" loadmoreoffset="10" style="">
      <cell v-for="(item, i) in todoLists" :key="i" @click="click(item, i)">
        <div class="panel">
          <text class="text">{{item}}</text>
        </div>
      </cell>
    </list>
  </div>
</template>

<script>
import { WxcMinibar } from 'weex-ui'
const modal = weex.requireModule('modal')
const LOADMORE_COUNT = 4

export default {
  components: { WxcMinibar },
  data () {
    return {
      todoLists: [1, 2, 3, 4, 5],
      finishedLists: []
    }
  },
  methods: {
    fetch (event) {
      modal.toast({ message: 'loadmore', duration: 1 })

      setTimeout(() => {
        const length = this.todoLists.length
        for (let i = length; i < length + LOADMORE_COUNT; ++i) {
          this.todoLists.push(i + 1)
        }
      }, 800)
    },
    click (item, i) {
      modal.toast({ message: 'Good', duration: 1 })
      this.finishedLists.push(item)
      this.todoLists.splice(i, 1)
    },
    minibarRightButtonClick () {
      modal.toast({ 'message': 'click rightButton!', 'duration': 1 })
    }
  }
}
</script>

<style scoped>
  .header {
    background-color: aquamarine;
    border-width: 2px;
  }
  .addButton {
    border-width: 2px;
    border-color: rgb(162, 217, 192);
  }
  .panel {
    width: 600px;
    height: 250px;
    margin-left: 75px;
    margin-top: 35px;
    margin-bottom: 35px;
    flex-direction: column;
    justify-content: center;
    border-width: 2px;
    border-style: solid;
    border-color: rgb(162, 217, 192);
    background-color: rgba(162, 217, 192, 0.2);
  }
  .text {
    font-size: 100px;
    text-align: center;
    color: #41B883;
  }
</style>

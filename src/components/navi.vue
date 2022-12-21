<template>
  <header>
    <div class="left"></div>
    <div class="right" @click="minimizeWin"><p>－</p></div>
    <div class="right" @click="maximizeWin" v-if="fullScreen == false">
      <p>□</p>
    </div>
    <div class="right" @click="unmaximizeWin" v-else><p>□</p></div>
    <div class="right" @click="closeWin"><p>×</p></div>
    <div class="mask" v-if="show">
      <div class="head">
        <h3>提示</h3>
        <div class="head-right" @click="show = false"><p>×</p></div>
      </div>
      <div class="content">
        <p>退出后无法正常使用，您要继续吗？</p>
      </div>
      <div class="btns">
        <div class="btn no" @click="show = false"><p>取消</p></div>
        <div class="btn yes" @click="closeapp"><p>确定</p></div>
      </div>
    </div>
  </header>
</template>

<script>
import { ipcRenderer } from "electron";
export default {
  data() {
    return {
      fullScreen: false,
      show: false,
    };
  },
  methods: {
    // 在页面methods使用
    // 最大化
    maximizeWin() {
      this.fullScreen = true;
      ipcRenderer.send("window-maximize");
    },
    // 退出最大化
    unmaximizeWin() {
      this.fullScreen = false;
      ipcRenderer.send("window-unmaximize");
    },
    // 最小化
    minimizeWin() {
      ipcRenderer.send("window-minimize");
    },
    // 退出程序
    closeWin() {
      this.show = true;
    },
    closeapp() {
      ipcRenderer.send("window-close");
    },
  },
};
</script>

<style lang="scss" scoped>
header {
  -webkit-app-region: drag;
  width: 100%;
  height: 6vh;
  background-color: brown;
  display: flex;
  align-items: center;
  position: relative;
  z-index: 9999999 !important;
  .left {
    flex: 1;
  }
  .right {
    -webkit-app-region: no-drag;
    width: 50px;
    height: 100%;
    color: rgba(255, 255, 255, 0.507);
    font-size: 30px;
    display: flex;
    align-items: center;
    justify-content: center;
    cursor: pointer;
    &:hover {
      background-color: rgb(129, 33, 33);
      color: white;
    }
  }
  .mask {
    position: absolute;
    left: 50%;
    transform: translateX(-50%);
    top: 200px;
    background-color: white;
    border: 1px solid #7e7e7e9c;
    border-radius: 10px;
    width: 500px;
    min-height: 220px;
    z-index: 99999999 !important;
    box-shadow: #7a7a7a 0px 0px 30px 0px;
    padding: 0px 20px;
    box-sizing: border-box;
    .head {
      width: 100%;
      text-align: left;
      padding: 20px 0px 10px 0px;
      box-sizing: border-box;
      border-bottom: 1px solid #7e7e7e1a;
      font-weight: bold;
      font-size: 22px;
      display: flex;
      align-items: center;
      justify-content: space-between;
      .head-right {
        -webkit-app-region: no-drag;
        color: rgba(53, 53, 53, 0.507);
        font-size: 30px;
        display: flex;
        align-items: flex-start;
        justify-content: center;
        cursor: pointer;
      }
    }
    .content {
      width: 100%;
      min-height: 130px;
      text-align: left;
      padding: 20px 0px 20px 0px;
      box-sizing: border-box;
      border-bottom: 1px solid #7e7e7e1a;
      font-size: 20px;
    }
    .btns {
      width: 100%;
      display: flex;
      align-items: center;
      justify-content: space-between;
      box-sizing: border-box;
      padding: 20px 130px;
      .btn {
        width: 80px;
        height: 40px;
        text-align: center;
        line-height: 40px;
        border-radius: 5px;
        box-sizing: border-box;
        cursor: pointer;
      }
      .yes {
        background-color: #1a73e8;
        color: #fff;
      }
      .no {
        border: 1px solid #dadce0;
        color: #1a73e8;
      }
    }
  }
}
</style>
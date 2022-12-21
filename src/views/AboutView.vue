<template>
  <div class="about">
    <img
      src="https://www.bing.com/th/id/OGC.dbfb4d57defa9f010ff6227073054dfb?pid=1.7&rurl=https%3a%2f%2fp.qqan.com%2fup%2f2021-3%2f16154396958249296.gif&ehk=ymOAkfzY4lq94%2bD7IXRCEDR0%2bi9HHEUM3Rpmgl3Kr2U%3d"
      alt=""
      srcset=""
    />
    <h1>第一点</h1>
    <h2>路由必须用哈希</h2>
    <h1>第二点</h1>
    <h2>最好配置淘宝镜像</h2>
    <h1>第三点</h1>
    <h2>尽量在添加electron-builder时就一次性安装electron</h2>
    <h2>否则版本不一致无法打包</h2>
    <h1>第四点</h1>
    <h2>打包时关闭所有进程，最好关闭所有后重新进入，直接打包</h2>
    <p>
      {{ content }}
    </p>
  </div>
</template>
<script>
export default {
  data() {
    return {
      content: ` 1.安装环境
       //安装淘宝镜像 
       npm install -g cnpm--registry=https://registry.npm.taobao.org
       //安装脚手架 
       npm install@vue/cli -g 
      //全局安装electron 
      npm install -g electron 添加打包工具 vue
      add electron-builder 
      运行electron npm run electron:serve // 如果报错删除node_modules依赖文件夹 重新npm install 打包exe包 npm run electron:build 
      2.自定义窗口化 在 background.js 文件中，初始化BrowserWindow
      时，添加属性 frame:false frame: false, // 无边框窗口 ，设置之后
      窗口将无法拖动，所以需要添加自义定拖拽区+最大化、最小化、关闭 /*
      设置拖拽区 */ -webkit-user-select: none; //防止拖动行为与选择文本冲突
      -webkit-app-region: drag; /* 设置拖拽区后，图标按钮无法点击
      必须设置其为不可拖拽才能触发点击事件 */ -webkit-app-region: no-drag;

      3.自定义最大化、退出最大化、最小化、关闭 在 background.js
      文件中，实例化createWindow对象里添加 
      // 退出程序
      ipcMain.on("window-close", function () { app.quit(); }); 
      // 最小化
      ipcMain.on("window-minimize", function () { win.minimize(); }); 
      // 最大化
      ipcMain.on("window-maximize", function () { win.maximize(); }); 
      //退出最大化 
      ipcMain.on("window-unmaximize", function () { win.unmaximize();}); 
      // 在页面methods使用 
      // 最大化 
      maximizeWin() { this.fullScreen = true;ipcRenderer.send("window-maximize"); },
      // 退出最大化 
      unmaximizeWin() {this.fullScreen = false; ipcRenderer.send("window-unmaximize"); },
      //最小化 
      minimizeWin() { ipcRenderer.send("window-minimize"); }, 
      // 退出程序
      closeWin() { ipcRenderer.send("window-close"); }, 
      注意！！！！
      自此之后会报错 在vue.config.js文件 module.exports中添加如下代码
      pluginOptions: { electronBuilder: { nodeIntegration: true, }, },
      .........监听应用退出 
      win.on("close", (e) => { e.preventDefault(); dialog
      .showMessageBox({ type: "info", // 弹出框类型 title: "提示", message:
      "确定退出", detail: "你确定要退出吗？", buttons: ["确定", "取消"], })
      .then((res) => { if (res.response === 0) { app.exit(); } else {
      e.preventDefault(); } }); }); 到这里打包基本结束了...
      4.打包之后的exe会自动安装，不能自己选择安装目录，就很懵 解决方法如下：
      在网上找了很多 都说是在package.json文件中的build节点添加如下配置
      但我新建多个vue文件后 发现package.json文件中根本没有build节点
      之后我在vue.config.js文件中添加 builderOptions就成功了
      //前3行是之前配置过的 pluginOptions: { electronBuilder: { nodeIntegration:
      true, builderOptions: { "appId": "appId", "productName":
      "productName",//项目名，也是生成的安装文件名，即productName.exe
      "copyright": "Copyright © 2022",//版权信息 "directories": { "output":
      "./dist"//输出文件路径，之前编译的默认是dist_electron }, "win": { "icon":
      "favicon.ico"//这里注意配好图标路径，注意需要256x256的 不然会报错 },
      "nsis": { "oneClick": false, // 一键安装
      "allowToChangeInstallationDirectory": true, // 允许修改安装目录 } } }, },
      更多配置可去官网了解.....`,
    };
  },
};
</script>

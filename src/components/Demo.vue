<template>
  <div>
    <div class="content m-b-50">
      <label for="serveId">服务器id：<input type="text" id="serveId" /></label>
      <label for="channelId">频道id：<input type="text" id="channelId" /></label>
    </div>
    <div class="content">
      <div class="editor">
        <Toolbar style="border-bottom: 1px solid #ccc" :editor="editor" :defaultConfig="toolbarConfig" :mode="mode" />
        <Editor style="height: 500px; overflow-y: hidden" v-model="html" :defaultConfig="editorConfig" :mode="mode" @onCreated="onCreated" @onChange="onChange" />
      </div>
      <div class="share-box">
        <span class="share-box-title">商品分享卡片示例：</span>
        <div class="card">
          <span class="card-title">好物分享</span>
          <div class="desc-box">
            <div class="desc" v-html="html"></div>
          </div>
        </div>
        <!-- <p>{{ desc }}</p> -->
      </div>
    </div>
  </div>
</template>
<script>
import { Editor, Toolbar } from '@wangeditor/editor-for-vue'
import { DomEditor } from '@wangeditor/editor'
export default {
  name: 'demo',
  components: { Editor, Toolbar },
  data() {
    return {
      editor: null,
      html: '',
      toolbarConfig: {
        excludeKeys: [],
      },
      editorConfig: {},
      mode: 'default', // or 'simple'
      desc: '',
    }
  },
  methods: {
    onCreated(editor) {
      // this.editor = Object.seal(editor) // 一定要用 Object.seal() ，否则会报错
      // console.log(DomEditor.getToolbar(editor))
      // // console.log(this.editor.getConfig().toolbarKeys)
      // // const curToolbarConfig = this.editor.getConfig()
      // // console.log(curToolbarConfig) // 当前菜单排序和分组
      // console.log(DomEditor.getToolbar(this.editor)) // 当前菜单排序和分组

      this.editor = Object.seal(editor) // 一定要用 Object.seal() ，否则会报错
      console.log(DomEditor.getToolbar(editor))
      console.log(editor.getAllMenuKeys())
      const curToolbarConfig = this.editor.getConfig()
      console.log(curToolbarConfig) // 当前菜单排序和分组
    },
    onChange() {
      this.desc = this.editor.getText()
    },
  },
  created() {
    let editorConfig = { placeholder: '请输入内容...', MENU_CONF: {} }
    editorConfig.MENU_CONF['insertImage'] = {
      onInsertedImage(imageNode) {
        // console.log('inserted image', imageNode)
        if (imageNode == null) return
        let { style } = imageNode
        // imageNode.style = 'width: 100%;'
        console.log('inserted image', style)
        // if (!style) {
        //   return 'width: 100%;'
        // }
        return '111'
      },
    }
    this.editorConfig = editorConfig
    // const curToolbarConfig = this.editor.getConfig(this.editor)
    // console.log(curToolbarConfig.toolbarKeys) // 当前菜单排序和分组
    // 模拟 ajax 请求，异步渲染编辑器
  },
  beforeDestroy() {
    const editor = this.editor
    if (editor == null) return
    editor.destroy() // 组件销毁时，及时销毁编辑器
  },
}
</script>
<style src="@wangeditor/editor/dist/css/style.css"></style>
<style scoped>
* {
  margin: 0;
  padding: 0;
}
.m-b-50 {
  margin-bottom: 50px;
}
.content {
  display: flex;
  justify-content: space-around;
}
.editor {
  width: 40%;
  border: 1px solid #ccc;
}
.share-box {
  width: 40%;
  justify-content: start;
  border-left: 1px solid #ccc;
  padding-left: 8%;
}
.share-box-title {
  display: block;
  text-align: left;
  color: rgb(150, 150, 150);
}
.card {
  display: flex;
  flex-direction: column;
  width: 70%;
  height: 85%;
  border-radius: 12px;
  overflow: hidden;
  margin-top: 30px;
  border: 1px solid #ccc;
}
.card-title {
  display: block;
  width: 100%;
  height: 48px;
  line-height: 48px;
  background: linear-gradient(to right, rgb(200, 223, 250), white);
  text-align: left;
  padding-left: 10px;
  color: rgba(122, 158, 183);
}
.desc-box {
  flex: 1;
  padding: 16px;
}
.desc {
  width: 100%;
  height: 90%;
  overflow-y: auto;
  word-break: break-all;
}

img {
  width: 100% !important;
}
</style>

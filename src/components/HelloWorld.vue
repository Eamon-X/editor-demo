<template>
  <div id="main"></div>
</template>

<script>
import E from 'wangeditor'
// const toolbarConfig = {                        /

// }
export default {
  name: 'HelloWorld',
  data() {
    return {
      editor: null,
      html: '<p>hello</p>',
      toolbarConfig: {},
      editorConfig: { placeholder: '请输入内容...' },
      mode: 'simple', // or 'simple'
    }
  },
  methods: {},
  mounted() {
    this.editor = new E('#main')
    this.editor.config.menus = ['fontSize', 'foreColor', 'emoticon', 'image', 'undo', 'redo']
    this.editor.create()
    console.log('@', this.editor)
    console.log(this.editor.config.menus)
    // 模拟 ajax 请求，异步渲染编辑器
    setTimeout(() => {
      this.html = '<p>模拟 Ajax 异步设置内容 HTML</p>'
    }, 1500)
  },
  beforeDestroy() {
    const editor = this.editor
    if (editor == null) return
    editor.destroy() // 组件销毁时，及时销毁编辑器
  },
}
</script>

<style src="@wangeditor/editor/dist/css/style.css"></style>

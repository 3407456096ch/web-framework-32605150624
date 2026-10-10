<template>
  <div class="note-card">
    <h3>我的第一条笔记</h3>
    <p>这是一个单文件组件</p>

    <!-- ✅插值三连（任务2第一步） -->
    <p>{{ message }}</p>
    <p>{{ message.toUpperCase() }}</p>
    <p>{{ 1 + 2 * 3 }}</p>

    <p>count = {{ count }} (3秒后自动变100 —— 不操作任何DOM)</p>

    <!-- v-text：原样输出文本，不会解析html标签 -->
    <p v-text="vtextStr"></p>
    <!-- v-html：解析html标签 -->
    <p v-html="vhtmlStr"></p>

    <p :title="tipMsg">我是 :title 绑定的悬停提示</p>

    <!-- class对象语法，count>0文字变绿色高亮 -->
    <p :class="{ highlight: count>0 }">count 大于 0 时这行变高亮（对象语法:class）</p>

    <!-- 按钮：内联语句、方法传参 -->
    <button @click="count++">count +1（内联语句）</button>
    <button @click="say('你好',$event)">say('你好',$event)（方法传参）</button>

    <p>实时展示 → 姓名:{{form.name}} | 性别:{{form.gender}} | 爱好:{{form.hobby}}</p>
    <input v-model="form.name" placeholder="输入姓名"/>
    <br>
    <input type="radio" v-model="form.gender" value="男"/>男
    <input type="radio" v-model="form.gender" value="女"/>女
    <br>
    <input type="checkbox" v-model="form.hobby" value="篮球"/>篮球
    <input type="checkbox" v-model="form.hobby" value="编程"/>编程

    <button @click="isShow = !isShow">切换显隐（观察DevTools元素面板）</button>

    <!-- v-if：条件为真才渲染DOM，假就直接删掉元素 -->
    <p v-if="isShow">v-if: 条件为真我才被"渲染"出来</p>
    <!-- v-show：DOM一直存在，只是css display:none隐藏 -->
    <p v-show="isShow">v-show: 我一直存在，只是被 display:none 藏起来</p>

    <select v-model="subject">
      <option value="语文">语文</option>
      <option value="数学">数学</option>
      <option value="Vue">Vue</option>
    </select>
  </div>
</template>

<script>
export default {
  name: "NoteCard",
  data() {
    return {
      message: "hello vue",
      count: 0,
      vtextStr: "<b>我是 v-text 的纯文本</b>",
      vhtmlStr: "<b>我是 v-html 解析出的加粗</b>",
      tipMsg: "我是title绑定的悬停提示",
      isShow: true,
      subject: "语文",
      form:{
        name:"",
        gender:"男",
        hobby:[]
      }
    }
  },
  mounted(){
    // 3秒后count变成100
    setTimeout(()=>{
      this.count = 100
    },3000)
  },
  methods:{
    say(msg, e){
      console.log(msg, e)
    }
  }
}
</script>

<style scoped>
.highlight{
  color: green;
  font-weight:bold;
}
.note-card{
  text-align:center;
  padding:20px;
  border:1px solid #333;
}
</style>

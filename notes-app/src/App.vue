<template>
  <div id="app">
    <h1>记事本 notes‑app · 第 2 章实验</h1>
    <NoteCard />
    <hr>
    <h2>📝记事本雏形（综合任务）</h2>

    <!-- 表单区域 -->
    <input
  v-model="newNote"
  placeholder="输入笔记内容"
  @keyup.enter="addNote"
  @keyup.esc="newNote=''"
/>
    <button @click="addNote">添加</button>
    <br>

    <!-- 优先级单选 -->
    <label><input type="radio" value="高" v-model="priority"/>高</label>
    <label><input type="radio" value="中" v-model="priority"/>中</label>
    <label><input type="radio" value="低" v-model="priority"/>低</label>
    <br>

    <!-- 标签复选 -->
    <label><input type="checkbox" value="待办" v-model="tags"/>待办</label>
    <label><input type="checkbox" value="灵感" v-model="tags"/>灵感</label>

    <p>实时展示 → 内容：{{newNote}}｜优先级：{{priority}}｜标签：{{tags.join('、')||'未选'}}</p >

    <!-- 笔记列表 -->
    
       <ul>
  <NoteCard v-for="note in notes" :key="note.id" :note="note"/>
</ul>

    <p v-if="notes.length===0">暂无笔记，快添加一条吧</p >
    <p v-show="notes.length>0">共 {{ notes.length }} 条</p >
<hr>
<h2>🎯事件实验室（2.4-2.5）</h2>
<EventLab />
  </div>
</template>

<script>
import NoteCard from './components/NoteCard.vue'
import EventLab from './components/EventLab.vue'

export default {
  components:{ NoteCard, EventLab },
  data(){
    return {
      newNote:'',
      priority:'中',
      tags:[],
      notes:[],
      nextId:1
    }
  },
  methods:{
    addNote(){
      // 判空，空白内容不添加
      if(!this.newNote.trim()) return
      this.notes.push({
        id: this.nextId++,
        text: this.newNote.trim(),
        priority: this.priority,
        tags: [...this.tags] // 数组展开复制，切断引用
      })
      this.newNote = '' // 添加完清空输入框
    }
  }
}
</script>

<style>
#app {
  max-width:700px;
  margin:20px auto;
  padding:0 20px;
}
li{
  margin:6px 0;
}
</style>
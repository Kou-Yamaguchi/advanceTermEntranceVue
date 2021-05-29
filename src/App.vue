<template>
  <div id="app">
    <div class="container">
      <div class="card">
        <div class="title">
          <p>Todo List</p>
        </div>
        <div class="todo">
          <div class="add">
            <input class="inputAdd" type="text" name="name" id="name" v-model="newText" />
            <button @click="addItem" class="buttonAdd">追加</button>
          </div>
          <div class="list">
            <div class="content" v-for="item in todoLists" :key="item.id">
              <input type="text" v-model="item.name">
              <button @click="updateItem(item.id, item.name)" class="buttonRenew">更新</button>
              <button @click="deleteItem(item.id)" class="buttonDelete">削除</button>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  props: ["id"],
  data() {
    return {
      newText: "",
      todoLists: [],
    };
  },
  methods: {
    async getTodo() {
      const resData = await axios.get("https://limitless-shelf-51102.herokuapp.com/api/todos/");
      this.todoLists = resData.data.data;
    },
    async addItem() {
      const sendData = {
        todo: this.newText,
      };
      await axios.post("https://limitless-shelf-51102.herokuapp.com/api/todos/", sendData);
      await this.getTodo();
    },
    async updateItem(id, name) {
      const updateData = {
        name: name,
      };
      await axios.put("https://limitless-shelf-51102.herokuapp.com/api/todos/" + id, updateData);
      await this.getTodo();
    },
    async deleteItem(id) {
      await axios.delete("https://limitless-shelf-51102.herokuapp.com/api/todos/" + id);
      await this.getTodo();
    }
  },
  created() {
    this.getTodo();
  },
};
</script>

<style>
html, body, div, span, object, iframe,
h1, h2, h3, h4, h5, h6, p, blockquote, pre,
abbr, address, cite, code,
del, dfn, em, img, ins, kbd, q, samp,
small, strong, sub, sup, var,
b, i,
dl, dt, dd, ol, ul, li,
fieldset, form, label, legend,
table, caption, tbody, tfoot, thead, tr, th, td,
article, aside, canvas, details, figcaption, figure,
footer, header, hgroup, menu, nav, section, summary,
time, mark, audio, video {
    margin:0;
    padding:0;
    border:0;
    outline:0;
    font-size:100%;
    vertical-align:baseline;
    background:transparent;
}

body {
    line-height:1;
}

article,aside,details,figcaption,figure,
footer,header,hgroup,menu,nav,section {
    display:block;
}

nav ul {
    list-style:none;
}

blockquote, q {
    quotes:none;
}

blockquote:before, blockquote:after,
q:before, q:after {
    content:'';
    content:none;
}

a {
    margin:0;
    padding:0;
    font-size:100%;
    vertical-align:baseline;
    background:transparent;
}

/* change colours to suit your needs */
ins {
    background-color:#ff9;
    color:#000;
    text-decoration:none;
}

/* change colours to suit your needs */
mark {
    background-color:#ff9;
    color:#000;
    font-style:italic;
    font-weight:bold;
}

del {
    text-decoration: line-through;
}

abbr[title], dfn[title] {
    border-bottom:1px dotted;
    cursor:help;
}

table {
    border-collapse:collapse;
    border-spacing:0;
}

/* change border colour to suit your needs */
hr {
    display:block;
    height:1px;
    border:0;  
    border-top:1px solid #cccccc;
    margin:1em 0;
    padding:0;
}

input, select {
    vertical-align:middle;
}

html {
  background-color: #15202b;
}
* {
  color: white;
  font-family: "Noto Sans JP";
}

/* ここから */
.container {
  height: 100vh;
  background-color: #2d197c;
  align-items: center;
  position: relative;
}

.card {
  background-color: #fff;
  width: 50vw;
  padding: 30px;
  margin: auto;
  border-radius: 10px;
  position: absolute;
  top: 25%;
  left: 25%;
}

.title p {
  color: black;
  font-weight: bold;
  font-size: 24px;
  margin-bottom: 15px;
}

.add {
  height: 38px;
  margin-bottom: 15px;
  display: flex;
}

.inputAdd {
  width: 80%;
  padding: 5px;
  border-radius: 5px;
  border: 1px solid #ccc;
  font-size: 14px;
  color: black;
}

button {
  padding: 8px 16px;
  font-weight: bold;
  background-color: #fff;
  transition: 0.4s;
  cursor: pointer;
  border-radius: 5px;
}

button:hover {
  color: white;
}

.buttonAdd {
  border: 2px solid #dc70fa;
  color: #dc70fa;
}

.buttonAdd:hover {
  background-color: #dc70fa;
}

.buttonRenew {
  border: 2px solid #fa9770;
  color: #fa9770;
}

.buttonRenew:hover {
  background-color: #fa9770;
}
</style>

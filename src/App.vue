<script>
import Main from './components/Main.vue'

export default {
  components: {
    Main,
  },
}
</script>

<template>
  <div class="app-shell">
    <el-container>
      <el-main class="site-main">
        <Main />
      </el-main>
    </el-container>

    <el-backtop :right="32" :bottom="56" />
  </div>
</template>

<style>
* {
  box-sizing: border-box;
}

html {
  background: #fbfbf8;
}

body {
  min-width: 320px;
  margin: 0;
  color: #17201f;
  background: #fbfbf8;
  text-rendering: optimizeLegibility;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}

#app,
.app-shell {
  min-height: 100vh;
}

.site-main {
  padding: 0;
}

h1 {
  font-family: "BoldFont", Times, "MyFont", Verdana, sans-serif;
  letter-spacing: 0px;
  font-size: 38px;
  margin: 0px;
  text-align: center;
}

h2,
h3,
h4,
h5,
h6 {
  font-family: "BoldFont", Times, Verdana, sans-serif;
  letter-spacing: 0px;
  font-size: 28px;
  margin: 0px;
  text-align: center;
}

.el-header {
  padding: 0px;
}

.el-footer {
  padding: 0px;
}

p,
li {
  font-family: "MyFont", Times, "Times New Roman", serif;
  font-size: 18px;
  line-height: 1.72;
  text-align: justify;
}

.custom-button {
  font-family: "BoldFont", "DemiFont", "Arial", sans-serif;
  font-size: 15px;
  font-weight: bold;
  color: #ffffff;
}

code {
  font-family: "Consolas", monospace;
  border-radius: 5px;
  padding: 2px 5px;
  background: #f2f2f2;
  color: black;
}

pre {
  border-radius: 5px;
  padding: 10px;
  background: #f2f2f2;
  line-height: 1.4rem;
}

pre:not(pre[id=bibtex]) {
  overflow-x: auto;
}

pre code {
  font-size: 16px;
  color: black;
  border: none;
  padding: 0px;
}

blockquote {
  border-left: 5px solid #bcbcbc;
  padding: 10px 20px 10px 20px;
  margin: 0px;
  background: #f6f6f6;
}

blockquote > p {
  margin-block-start: 0.5em;
  margin-block-end: 0.5em;
}

a {
  color: #1f6f95;
  text-decoration: none;
}

a:hover {
  color: #14544e;
  border-bottom: 1px dotted currentColor;
}

p > img {
  width: 80%;
  display: block;
  margin: 0 auto;
  border-radius: 10px;
  box-shadow: 1px 1px 4px 1px #afafaf;
}

table {
  border-collapse: collapse;
  width: max-content;
  max-width: 100%;
  margin: 0 auto;
  display: block;
  overflow-x: auto;
}

thead {
  border-bottom-width: 1px;
  border-top-width: 2px;
  border-left-width: 0px;
  border-right-width: 0px;
  border-style: solid;
  border-color: rgb(0 0 0);
}

tbody tr:last-child {
  border-bottom-width: 2px;
  border-top-width: 0px;
  border-left-width: 0px;
  border-right-width: 0px;
  border-style: solid;
  border-color: rgb(0 0 0);
}

th,
td {
  padding-left: 1rem;
  padding-right: 1rem;
}

.katex-display {
  overflow-x: auto;
  overflow-y: hidden;
}
</style>

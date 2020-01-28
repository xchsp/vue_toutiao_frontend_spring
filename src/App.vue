<template>
  <div id="app">
    <keep-alive include="homePage">
      <router-view />
    </keep-alive>
  </div>
</template>

<script>
export default {
  name: 'App'
}
</script>

<style lang="less">
@import url(http://at.alicdn.com/t/font_1426139_h6vn3jbl5q.css);
* {
  margin: 0;
  padding: 0;
}
a {
  color: inherit;
}
a:hover {
  text-decoration: none;
}
ul,
li,
ol {
  list-style: none;
}
</style>

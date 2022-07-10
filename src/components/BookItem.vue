<template>
  <li>
    {{book.title}} : {{book.author}}
    <span v-if="book.finishedReading === 'read'">Read</span>
    <span v-else-if="book.finishedReading === 'reading'">Reading</span>
    <span v-else>Not Read</span>

    <span v-if="book.liked" style="color:red">❤</span>
  </li>
</template>

<script>
export default {
  name: 'BookItem',
  props: ['book'],
};
</script>

<style>
li {
  display: block;
  margin: 0 10px;
}
</style>

<template>
  <li>
    {{book.title}} : {{book.author}}
    <span v-if="book.finishedReading === 'read'" style="font-weight:bold">Read</span>
    <span v-else-if="book.finishedReading === 'reading'" style="font-weight:bold">Reading</span>
    <span v-else style="font-weight:bold">Not Read</span>

    <span v-if="book.liked">❤</span>
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

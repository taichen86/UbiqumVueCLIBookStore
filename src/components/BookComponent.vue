<template>
    <div id="BookComponent">
    <div> {{ book.title }} </div>
    <div> {{ book.description }} </div>
    </div>
</template>

<script>
export default {
  name: 'BookComponent',
  props: {
      book: Object
  }
}
</script>

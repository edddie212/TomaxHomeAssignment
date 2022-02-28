<template>
    <div @drop="onDrop($event, 2)" @dragover.prevent class="card mb-4" style="background: #e8e8e8; height: 100%;"></div>
</template>

<script>
export default {
  name: "MainContent"
}
</script>

<style scoped>

</style>
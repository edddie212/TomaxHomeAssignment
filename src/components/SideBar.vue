<template>

<div v-for="user in myUsers" :key="user.user">
  <div class="my-card card bg-light mb-3" >
    <div class="card-header" dir="rtl">  {{user.user}} | {{user.name}}</div>
    <div class="card-body">
      <div class='drag-el' draggable="true" @dragstart="startDrag($event, item)"
           :style="{backgroundImage: 'url('+user.picture+')'}"
           style="width: 124px; height: 124px; background-size: contain;"></div>
    </div>
  </div>
</div>






</template>

<script>
import axios from 'axios';

export default {
  name: "SideBar",

}
</script>

<style scoped>
.my-card {
  max-width: 18rem;
  max-height: 12rem;
}

.drop-zone {
  background-color: #eee;
  margin-bottom: 10px;
  padding: 10px;
}

.drag-el {
  background-color: #fff;
  margin-bottom: 10px;
  padding: 5px;
}
</style>
<template>
  <div style="padding: 10px;">
    <a-card :title="title" style="width: 300px;" >
      <template #extra><a href="#">more</a></template>
      <img :src="imgsrc" alt="老大" style="width: 250px;">
      <p style="font-size: medium;">{{ description }}</p>
      <div class="time" style="color: #999;position: absolute;bottom: 20px;left: 20px;font-size: 12px;">{{ time }}</div>
      <div class="owner" style="color: #999;position: absolute;bottom: 20px;right: 20px;font-size: 12x;">{{ owner }}</div>
    </a-card>
  </div>

</template>

  <script>
  export default {
    name: 'CardItem',
      props: {
          title: String,
          time: String,
          owner: String,
          imgsrc: String,
          description: String
      }
  }
  </script>

  <style>

  </style>

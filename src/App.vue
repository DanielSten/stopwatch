<template>
  <div class="wrapper">
    <div class="container">
      <stopwatch v-for="item in items"></stopwatch>
      <div class="block_add-stopwatch" @click="add">
        <i class='bx bx-plus'></i>
      </div>
  </div>
  </div>
</template>

<script>
import stopwatch from "./components/stopwatch.vue";

export default {
  components:{
    stopwatch,
  },
  data() {
    return{
      items: [],
    }
  },
  methods: {
    add() {
      this.items.push(stopwatch);
    }
  }
}
</script>

<style scoped>
.wrapper{
  width: 100%;
  min-height: 100vh;
  max-height: 100%;
  background-color: rgba(53, 54, 56, 1);
  padding: 100px 0;
}
.container{
  width: 825px;
  display: flex;
  flex-wrap:wrap;
  margin: 0 auto;
}

.block_add-stopwatch{
  width: 225px;
  height: 120px;
  background-color: rgba(105, 105, 105, 1);
  margin: 0 25px;
  text-align: center;
  color: rgba(158, 158, 158, 1);
}
.block_add-stopwatch:hover{
  color: #FFFFFF;
}
.bx-plus{
  font-size: 40px;
  line-height: 120px;
}

@media (max-width: 1024px) {
  .container{
    width: 550px;
  }
}
@media (max-width: 768px) {
  .container{
    width: 275px;
  }
}
</style>

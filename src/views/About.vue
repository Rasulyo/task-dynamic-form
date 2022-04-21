<template>
  <div class="about">
    <div class="block">
      <h4>Персональные данные</h4>
      <ul class="content" v-for="item in list" :key="item.name">
        <li class="parent">{{ item.name }} ,{{ item.age }}</li>
        <p>Дети</p>
        <div class="content-block">
          <p class="content-name" v-for="child in item.child" :key="child.name">
            <span class="item">{{ child.name }}, {{ child.age }}</span>
          </p>
        </div>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  name: "About",
  data() {
    return {
      list: [],
    };
  },
  mounted() {
    if (!localStorage.getItem("info")) {
      localStorage.setItem("info", "[]");
    }
    this.list = JSON.parse(localStorage.getItem("info"));
  },
};
</script>

<style scoped>
.about {
  text-align: center;
  max-width: 600px;
  margin: 0 auto;
  padding: 20px;
}
.block{
  width: 400px;
  display: flex;
  justify-content: flex-start;
  flex-direction: column;
  text-align: justify;
}
.content {
  list-style: none;
  color: black;
  display: flex;
  justify-self: start;
  flex-direction: column;
  padding: 0;
}
.parent {
  font-weight: bold;
  font-size: 16px;
}
.content-name {
  display: flex;
  list-style: none;
}

.item {
  display: flex;
  padding: 5px 15px;
  border-radius: 5px;
  font-weight: 500;
  max-width: 100%;
  background: gray;
  color: white;
}
</style>

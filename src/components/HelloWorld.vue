<template>
  <div class="hello">
    <div class="header">
      <h1>Персональные данные</h1>
      <input class="parent-class" v-model="nameOfPerson" type="text" placeholder="Имя" />
      <input
        class="parent-class"
        v-model="ageOfPerson"
        type="number"
        placeholder="Возраст"
      />
      <div class="content-btn">
        <span>Дети (Макс 5) </span>
        <button @click="addInput" class="add-btn" v-show="inputs.length <= 4">
          <img src="../assets/Union.png" alt="union" /> Добавить ребенка
        </button>
      </div>
      <div class="content" v-for="(input, mod) in inputs" :key="mod">
        <input
          v-if="isVisible"
          class="form"
          type="text"
          v-model="input.name"
          placeholder="Имя ребёнка"
        />
        <input
          v-if="isVisible"
          class="form"
          type="text"
          v-model="input.age"
          placeholder="Возраст ребёнка"
        />
        <span>
          <button
            class="remove-btn"
            @click="remove(mod)"
            v-show="mod || (!mod && inputs.length > 0)"
          >
            Удалить
          </button>
        </span>
      </div>
    </div>
    <button class="save-btn" @click="addChild">Сохранить</button>
    <button class="clean-btn" @click="cleanData">Очистить данные</button>
  </div>
</template>

<script>
export default {
  name: "HelloWorld",
  data() {
    return {
      nameOfPerson: "",
      ageOfPerson: "",
      isVisible: false,
      inputs: [],
    };
  },
  methods: {
    addChild() {
      const obj = {
        name: this.nameOfPerson,
        age: this.ageOfPerson,
        child: this.inputs.map((a, b) => {
          const obj = {
            name: a.name,
            age: a.age,
          };
          return obj;
        }),
      };
      if (!localStorage.getItem("info")) {
        localStorage.setItem("info", "[]");
      }
       
      const data = JSON.parse(localStorage.getItem("info"));
      data.push(obj);
      localStorage.setItem("info", JSON.stringify(data));
      alert('Вы сохранили персональные данные');
      (this.nameOfPerson = ""), (this.ageOfPerson = "");
      this.inputs.map((a, b) => {
        return (a.name = "");
      }),
        this.inputs.map((a, b) => {
          return (a.age = "");
        });
    },
    cleanData() {
      if (!localStorage.getItem("info")) {
        console.log('Data is empty')
      }
      localStorage.removeItem('info')
    },
    addInput() {
      this.isVisible = true;
      this.inputs.push({ name: "" });
    },

    remove(index) {
      this.inputs.splice(index, 1);
    },
  },
};
</script>

<style scoped>
.hello {
  box-sizing: border-box;
  margin: 0 auto;
}
.header {
  display: flex;
  flex-direction: column;
  align-content: space-between;
  width: 620px;
  margin: 0 auto;
}
.content {
  display: Flex;
  color: rebeccapurple;
  justify-content: center;
  align-self: center;
  position: relative;
}

.content-btn {
  display: flex;
  justify-content: space-around;
  align-items: center;
}
.content-btn > span {
  font-size: 16px;
  font-weight: 500;
  line-height: 24px;
  color: black;
}
.parent-class {
  width: 600px;
  margin: 10px;
  line-height: 24px;
  font-size: 14px;
  height: 50px;
  border: 1px solid #f1f1f1;
  border-radius: 4px;
}
.add-btn {
  width: 200px;
  height: 40px;
  border-radius: 20px;
  border: none;
  display: flex;
  border: 1.5px solid #01a7fd;
  background: white;
  align-items: center;
  color: #01a7fd;
  outline: none;
}
.add-btn img {
  padding: 0 10px;
}
.form {
  color: #111111;
  width: 250px;
  height: 35px;
  outline: none;
  border: 1px solid #f1f1f1;
  margin: 5px;
  line-height: 24px;
  font-size: 14px;
  border-radius: 5px;
}
.remove-btn {
  width: 50px;
  margin: 15px 5px;
  font-size: 14px;
  border: none;
  color: skyblue;
  background: transparent;
}
.save-btn {
  width: 140px;
  margin: 20px 0;
  height: 40px;
  color: white;
  background: #01a7fd;
  border-radius: 50px;
  border: none;
  cursor: pointer;
}
.clean-btn {
  width: 140px;
  margin: 20px 0;
  height: 40px;
  color: white;
  background: #fd6601;
  border-radius: 50px;
  border: none;
  cursor: pointer;
}
.clean-btn:hover, .save-btn:hover {
   width: 138px;
  height: 38px;
  border: 1px solid gray;
}
</style>

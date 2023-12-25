<template>
  <div class="home">
    <div class="row g-4 py-5 row-cols-1 row-cols-lg-3">
      <div class="col d-flex align-items-start">
        <div
          class="icon-square text-body-emphasis bg-body-secondary d-inline-flex align-items-center justify-content-center fs-4 flex-shrink-0 me-3"
        ></div>
        <div>
          <h3 class="fs-2 text-body-emphasis">Создание продукта</h3>
          <button class="btn btn-primary" @click="pushedProduct">
            Создать
          </button>
        </div>
      </div>
      <div class="col d-flex align-items-start">
        <div
          class="icon-square text-body-emphasis bg-body-secondary d-inline-flex align-items-center justify-content-center fs-4 flex-shrink-0 me-3"
        ></div>
        <div>
          <h3 class="fs-2 text-body-emphasis">Добавление сотрудника</h3>
          <button class="btn btn-primary" @click="pushedEmployee">
            Добавить
          </button>
        </div>
      </div>
    </div>

    <UserEmployee v-if="this.productButton" modalWindowType="productCreation" />

    <UserEmployee
      v-if="this.employeeButton"
      modalWindowType="employeeCreation"
    />
  </div>
</template>
<script>
import UserEmployee from "./components/UserEmployee.vue";
export default {
  // setup() {
  //   let productButton = false;
  //   let employeeButton = false;
  //   return productButton, employeeButton;
  // },
  data() {
    return {
      productButton: false,
      employeeButton: false,
    };
  },
  components: {
    UserEmployee,
  },
  methods: {
    pushedProduct() {
      this.productButton = !this.productButton;
      this.employeeButton = false;
    },
    pushedEmployee() {
      this.employeeButton = !this.employeeButton;
      this.productButton = false;

    },
  },
};
</script>
<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}

nav {
  padding: 30px;
}

nav a {
  font-weight: bold;
  color: #2c3e50;
}

nav a.router-link-exact-active {
  color: #42b983;
}
</style>

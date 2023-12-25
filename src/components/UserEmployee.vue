<template>
  <div class="border rounded border-dark px-3 py-3 mx-5 my-5">
    <form @submit.prevent="sendData(this.sendingData)" name="userForm">
      <!-- Окно 1 -->
      <div v-if="modalWindowType == 'productCreation'" class="firstWindow">
        <div class="mb-3">
          <label for="managerSelect" class="form-label">Менеджер</label>
          <select
            v-model="selected"
            @input="inputManager"
            class="form-select"
            id="managerSelect"
            form="userForm"
          >
            <option v-for="manager in managers" v-bind:key="manager">
              {{ manager.name }}
            </option>
          </select>
        </div>

        <div class="mb-3">
          <input
            v-bind:value="productTitle"
            @input="inputProductTitle"
            type="text"
            id="productTitle"
            class="form-control"
            placeholder="Название продукта"
          />
        </div>

        <div class="mb-3">
          <input
            v-bind:value="jiraLink"
            @input="inputJiraLink"
            type="text"
            id="jiraLink"
            class="form-control"
            placeholder="Ссылка в Jira"
          />
        </div>

        <div class="mb-3">
          <label for="domen">Домен</label>
          <select
            v-model="selected"
            @input="inputDomen"
            class="form-select"
            id="domen"
            form="userForm"
          >
            <option v-for="domen in domens" v-bind:key="domen">
              {{ domen.title }}
            </option>
          </select>
        </div>
      </div>

      <!-- Окно 2 -->
      <div class="mb-3">
        <div v-if="modalWindowType == 'employeeCreation'" class="secondWindow">
          <div class="mb-3">
            <label for="employeeSelect">Сотрудник</label>
            <select
              v-model="selected"
              @input="inputEmployee"
              class="form-select"
              id="employeeSelect"
              form="userForm"
            >
              <option v-for="employee in employees" v-bind:key="employee">
                {{ employee.name }}
              </option>
            </select>
          </div>
          <div class="mb-3">
            <label for="employeesSupervisorSelect"
              >Руководитель сотрудника</label
            >
            <select
              v-model="selected"
              @input="inputSupervisor"
              class="form-select"
              id="employeesSupervisorSelect"
              form="userForm"
            >
              <option v-for="supervisor in supervisors" v-bind:key="supervisor">
                {{ supervisor.name }}
              </option>
            </select>
          </div>

          <div class="mb-3">
            <label for="rateType">Тип ставки</label>
            <select
              v-model="selected"
              @input="inputRateType"
              class="form-select"
              id="rateType"
              form="userForm"
            >
              <option v-for="rateType in rateTypes" v-bind:key="rateType">
                {{ rateType.title }}
              </option>
            </select>
          </div>

          <div class="mb-3">
            <label for="businessPartSelect">Бизнес-единица</label>
            <select
              v-model="selected"
              @input="inputBusinessPart"
              class="form-select"
              id="businessPartSelect"
              form="userForm"
            >
              <option
                v-for="businessPart in businessParts"
                v-bind:key="businessPart"
              >
                {{ businessPart.title }}
              </option>
            </select>
          </div>
          <div class="mb-3">
            <input
              v-bind:value="capitalizationPercent"
              @input="inputCapitalizationPercent"
              type="number"
              placeholder="Процент капитализации"
              id="capitalizationPercent"
              class="form-control"
              form="userForm"
            />
          </div>

          <div class="mb-3">
            <input
              v-bind:value="position"
              @input="inputPosition"
              type="text"
              placeholder="Должность"
              id="position"
              class="form-control"
              form="userForm"
            />
          </div>
        </div>
      </div>

      <div class="mb-3">
        <input
          class="form-control btn btn-primary"
          @click="sendData"
          type="submit"
          value="Создать"
        />
      </div>
    </form>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "UserEmployee",
  props: {
    modalWindowType: String,
    required: true,
  },
  data() {
    return {
      managers: [
        { id: 0, name: "Michael" },
        { id: 1, name: "Sarah" },
        { id: 2, name: "Genry" },
        { id: 3, name: "Josef" },
        { id: 4, name: "Anna" },
      ],
      domens: [
        { id: 0, title: "Бэк-офис" },
        { id: 1, title: "Техплатформа" },
        { id: 2, title: "Офис больших данных" },
      ],
      businessParts: [
        { id: 0, title: "MVM" },
        { id: 1, title: "MTech" },
      ],
      employees: [
        { id: 0, name: "Michael" },
        { id: 1, name: "Sarah" },
        { id: 2, name: "Genry" },
        { id: 3, name: "Lori" },
        { id: 4, name: "Salma" },
        { id: 5, name: "Jack" },
        { id: 6, name: "Josef" },
        { id: 7, name: "Anna" },
      ],
      supervisors: [
        { id: 0, name: "Christian" },
        { id: 1, name: "David" },
        { id: 2, name: "Lori" },
        { id: 3, name: "Salma" },
        { id: 4, name: "Jack" },
      ],
      rateTypes: [
        { id: 0, title: "орех" },
        { id: 1, title: "сорех" },
      ],
      manager: "",
      domen: "",
      employee: "",
      supervisor: "",
      businessPart: "",
      productTitle: "",
      jiraLink: "",
      rateType: "",
      capitalizationPercent: 0,
      position: "",
      sendingData: [],
    };
  },
  methods: {
    inputManager(event) {
      this.manager = event.target.value;
    },
    inputDomen(event) {
      this.domen = event.target.value;
    },
    inputEmployee(event) {
      this.employee = event.target.value;
    },
    inputSupervisor(event) {
      this.supervisor = event.target.value;
    },
    inputRateType(event) {
      this.rateType = event.target.value;
    },
    inputBusinessPart(event) {
      this.businessPart = event.target.value;
    },
    inputProductTitle(event) {
      this.productTitle = event.target.value;
    },
    inputJiraLink(event) {
      this.jiraLink = event.target.value;
    },
    inputRateType(event) {
      this.rateType = event.target.value;
    },
    inputCapitalizationPercent(event) {
      this.capitalizationPercent = event.target.value;
    },
    inputPosition(event) {
      this.position = event.target.value;
    },
    sendData(sendingData) {
      if (this.modalWindowType == "productCreation") {
        sendingData = [
          this.manager,
          this.productTitle,
          this.jiraLink,
          this.domen,
        ];
      } else if (this.modalWindowType == "employeeCreation") {
        sendingData = [
          this.employee,
          this.supervisor,
          this.rateType,
          this.businessPart,
          this.capitalizationPercent,
          this.position,
        ];
      }

      axios
        .post("/api/" + this.modalWindowType, sendingData)
        .then((res) => {
          console.log("SENDING DATA: " + sendingData);
          console.log(res);
        })
        .catch((error) => {
          console.log(error.response.data);
          console.log("SENDING DATA: " + sendingData);
        });
    },
  },
};
</script>

<style scoped></style>

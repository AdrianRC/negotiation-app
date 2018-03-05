<template>
  <div id="app">
    <div id="negotiationWidget">
      <div v-if="!finished">
        <div id="tabs">
          <button class="selector" @click="selected = 'Employer'" :class="{unselectedTab: selected === 'Employee'}">Employer Tab</button>
          <button class="selector" @click="selected = 'Employee'" :class="{unselectedTab: selected === 'Employer'}">Employee Tab</button>
        </div>
        <div id="form">
          <keep-alive>
            <component :is="selected" @salarySelected="handleSelect($event)"></component>
          </keep-alive>
        </div>
      </div>
      <result v-else :employer="salaries.employer" :employee="salaries.employee"></result>
    </div>
  </div>
</template>

<script>
import Employee from "./components/Employee";
import Employer from "./components/Employer";
import Result from "./components/Result";

export default {
  name: "app",
  data() {
    return {
      selected: "Employer",
      salaries: {
        employee: undefined,
        employer: undefined
      },
      finished: false
    };
  },
  components: {
    Employee,
    Employer,
    Result
  },
  methods: {
    handleSelect(payload) {
      // adds the chosen salary to the corresponding author.
      this.salaries[payload.author] = payload.value;
      // if both salaries are selected, change state to finished.
      if (this.salaries.employee && this.salaries.employer) {
        this.finished = true;
      }
    }
  }
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  display: flex;
  align-items: center;
  justify-content: center;
  height: 100vh;
}

#negotiationWidget {
  border: 1px solid black;
  width: 600px;
  border-radius: 3px;
}

#form {
  display: flex;
  align-items: center;
  justify-content: center;
  height: 400px;
}

#tabs {
  display: flex;
  height: 50px;
}

.selector {
  width: 50%;
  font-size: 18px;
  background: none;
  outline: none;
  border: none;
  color: #2c3e50;
}

h1,
h2 {
  font-weight: normal;
}

h1 {
  color: #42b983;
}

.unselectedTab {
  background-color: lightgreen;
  color: white;
}

.submit {
  border: 1px solid lightgreen;
  background: none;
  display: block;
  width: 100px;
  margin: 10px auto;
  font-size: 14px;
}

input[type="number"] {
  font-size: 14px;
  text-align: center;
  width: 80px;
  outline: none;
  border: 1px solid lightgreen;
  border-radius: 3px;
}
</style>

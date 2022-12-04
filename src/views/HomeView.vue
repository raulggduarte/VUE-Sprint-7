<template>
  <div class="home">
    <RouteBtn :adress="`/`" :text="`Torna a l'inici`" class="goBackBtn" />
    <div class="main">
      <Home
        :budgetsList="budgetsList"
        @update-budgets-list="updateBudgetsList"
      />
      <BudgetsList v-show="budgetsList.length > 0" :budgetsList="budgetsList" />
    </div>
  </div>
</template>

<script>
// @ is an alias to /src
import Home from "@/components/Home";
import RouteBtn from "@/components/RouteBtn";
import BudgetsList from "@/components/BudgetsList";

export default {
  name: "HomeView",
  components: {
    Home,
    RouteBtn,
    BudgetsList,
  },
  data() {
    return {
      adress: String,
      text: String,
      budgetsList: [],
    };
  },
  methods: {
    updateBudgetsList(newBudget) {
      this.budgetsList.push(newBudget);
    },
  },
};
</script>

<style>
.home {
  display: flex;
  flex-direction: column;
  align-items: center;
}
.goBackBtn {
  margin: 20px 0 0 20px;
  align-self: flex-start;
}
.main {
  display: flex;
}
</style>

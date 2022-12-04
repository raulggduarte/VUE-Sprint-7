<template>
  <div class="budgetsList">
    <h3>Llistat de pressupostos</h3>
    <OrderBtns v-show="budgetsList.length > 1" @order-budgets="orderBudgets" />
    <SearchBudget v-show="budgetsList.length > 1" @budget-name="updateBudgetName"/>
    <ul
      v-for="budget in orderedBudgetsList"
      :key="budget.id"
      class="p-0"
      v-show="!budgetName || budget.name.toLowerCase().includes(budgetName.toLowerCase())"
    >
      <li class="card px-4 py-2">
        <div>
          <b>Nom: {{ budget.name }}</b>
        </div>
        <div class="small ps-1">
          <div>ID: {{ budget.id }}</div>
          <div>Client: {{ budget.client }}</div>
          <div>Data: {{ budget.date }}</div>
          <div>
            Productes:
            <ul v-for="product in budget.products" :key="product.id">
              <li>
                <div>ID del producte: {{ product.id }}</div>
                <div>Nom del producte: {{ product.name }}</div>
                <div>Preu del producte: {{ product.updatedPrice }}</div>
                <div v-show="product.hasOptions">
                  Opcions seleccionades:
                  <div>
                    <ul v-for="option in product.options" :key="option.id">
                      <li>
                        <div>{{ option.qty }} {{ option.name }}</div>
                      </li>
                    </ul>
                  </div>
                </div>
              </li>
            </ul>
          </div>
        </div>
        <div>
          <b>Preu total: {{ budget.price }}</b>
        </div>
      </li>
    </ul>
  </div>
</template>

<script>
import OrderBtns from "./OrderBtns";
import SearchBudget from "./SearchBudget";

export default {
  name: "BudgetsList",
  props: {
    budgetsList: Object,
  },
  components: {
    OrderBtns,
    SearchBudget,
  },
  data() {
    return {
      orderedBudgetsList: this.budgetsList,
      budgetName: "",
    };
  },
  methods: {
    orderBudgets(typeOfOrder) {
      console.log(this.budgetName);
      if (typeOfOrder === "alfa") {
        this.orderedBudgetsList = [...this.budgetsList].sort((a, b) => {
          const nameA = a.name.toUpperCase();
          const nameB = b.name.toUpperCase();
          if (nameA < nameB) {
            return -1;
          }
          if (nameA > nameB) {
            return 1;
          }
          return 0;
        });
      } else if (typeOfOrder === "date") {
        this.orderedBudgetsList = [...this.budgetsList].sort((a, b) => {
          const dateA = a.date;
          const dateB = b.date;
          if (dateA < dateB) {
            return -1;
          }
          if (dateA > dateB) {
            return 1;
          }
          return 0;
        });
      } else {
        this.orderedBudgetsList = [...this.budgetsList];
      }
    },
    updateBudgetName(newName) {
      this.budgetName = newName;
    }
  },
};
</script>

<style scoped>
.budgetsList {
  margin: 20px;
}
h3 {
  margin: 30px 0 20px 0;
}
li {
  list-style-type: none;
}
</style>
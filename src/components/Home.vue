<template>
  <div class="productList">
    <h1>¿Què vols fer?</h1>
    <form @submit="onSubmit" class="productInput">
      <input
        type="text"
        name="budgetName"
        placeholder="Nom del pressupost"
        v-model="budgetName"
        class="inputForm"
      />
      <input
        type="text"
        name="clientName"
        placeholder="Nom del client"
        v-model="clientName"
        class="inputForm"
      />
      <div v-for="product in products" :key="product.id">
        <input
          class="course"
          type="checkbox"
          :id="product.id"
          :value="product.name"
          @click="updateProductSelection(product)"
          v-model="product.selected"
        />
        <!-- </router-link> -->
        <label :for="product.id"
          >{{ product.description }} ({{ product.price }})</label
        >
        <Transition name="bounce">
          <Panel
            v-show="product.selected && product.hasOptions"
            :product="product"
            @update-options="updateOptions"
          />
        </Transition>
      </div>
      <h3>Preu: {{ totalBudget }}€</h3>
      <input
        type="submit"
        value="Envia pressupost"
        class="btn btn-outline-dark"
      />
    </form>
  </div>
</template>

<script>
import Panel from "./Panel";

export default {
  name: "Home",
  components: {
    Panel,
  },
  props: {
    budgetsList: Array,
  },
  data() {
    return {
      totalBudget: 0,
      products: [
        {
          id: 0,
          name: "web",
          description: "Una pàgina web",
          price: 500,
          updatedPrice: 500,
          selected: false,
          hasOptions: true,
          options: [
            {
              id: 0,
              tag: "numPag",
              name: "pagines",
              text: "Nombre de pàgines",
              qty: 0,
              modalText:
                "Aquí has d'indicar el nombre de pàgines de la teva web",
            },
            {
              id: 1,
              tag: "numLang",
              name: "llengues",
              text: "Nombre d'idiomes",
              qty: 0,
              modalText:
                "Aquí has d'indicar en quants idiomes voldràs la teva web",
            },
          ],
          optionsPrice: 30,
        },
        {
          id: 1,
          name: "seo",
          description: "Una consultoria SEO",
          price: 300,
          updatedPrice: 300,
          selected: false,
          hasOptions: false,
          options: [
            { id: 0, tag: "", name: "", text: "", qty: 0, modalText: "" },
            { id: 1, tag: "", name: "", text: "", qty: 0, modalText: "" },
          ],
          optionsPrice: undefined,
        },
        {
          id: 2,
          name: "ads",
          description: "Una campanya de Google Ads",
          price: 200,
          updatedPrice: 200,
          selected: false,
          hasOptions: false,
          options: [
            { id: 0, tag: "", name: "", text: "", qty: 0, modalText: "" },
            { id: 1, tag: "", name: "", text: "", qty: 0, modalText: "" },
          ],
          optionsPrice: undefined,
        },
      ],
      productSelection: [],
      budgetName: "",
      clientName: "",
    };
  },
  methods: {
    updateBudget() {
      this.totalBudget = 0;

      this.products.forEach((product) => {
        if (product.hasOptions) {
          product.updatedPrice = 0;

          let optionsPrice = 1;

          product.options.forEach((option) => (optionsPrice *= option.qty));

          optionsPrice *= product.optionsPrice;

          product.updatedPrice = product.price + optionsPrice;
        }
      });

      this.productSelection.forEach(
        (product) =>
          (this.totalBudget = this.totalBudget + product.updatedPrice)
      );
    },

    updateProductSelection(product) {
      product.selected = !product.selected;

      this.productSelection = this.products.filter(
        (el) => el.selected === true
      );

      this.updateBudget();
    },

    startProductSelection() {
      this.productSelection = this.products.filter(
        (el) => el.selected === true
      );
      this.updateBudget();
    },

    updateOptions(optionQty, productID, optionId) {
      this.products[productID].options[optionId].qty = optionQty;
      this.updateBudget();
    },

    onSubmit(e) {
      e.preventDefault();

      if (!this.budgetName || !this.clientName) {
        alert("Si us plau, afegeix un nom del pressupost i del client.");
        return;
      }

      if (this.productSelection.length <= 0) {
        alert("Si us plau, sel·lecciona, al menys, un producte.");
        return;
      }

      const newBudget = {
        id: Date.now(),
        date: new Date(Date.now()).toLocaleDateString(),
        name: this.budgetName,
        client: this.clientName,
        products: this.productSelection,
        price: this.totalBudget,
      };

      this.$emit("update-budgets-list", newBudget);

      this.productSelection = [];
      this.products.forEach((el) => {
        el.selected = false;
        el.updatedPrice = el.price;
      });
      this.budgetName = "";
      this.clientName = "";
      this.updateBudget();
    },
    setQueryParams() {
      const query = this.$route.query;
      const queryAsArray = Object.entries(query);
      this.products.forEach((product) => {
        queryAsArray.forEach((query) => {
          if (query[0] === product.name) {
            product.selected = query[1] === "true";
          }
          if (query[0] === "preu") {
            this.totalBudget = Number(query[1]);
          }
          if (product.hasOptions) {
            product.options.forEach((option) => {
              if (option.name === query[0]) {
                option.qty = Number(query[1]);
              }
            });
          }
        });
      });
    },
  },
  computed: {
    queryParams({ products, totalBudget }) {
      const queryParamsArray = [];
      products.forEach((product) => {
        if (product.hasOptions) {
          queryParamsArray.push([product.name, product.selected]);
          product.options.forEach((option) => {
            queryParamsArray.push([option.name, option.qty]);
          });
        } else {
          queryParamsArray.push([product.name, product.selected]);
        }
      });
      queryParamsArray.push(["preu", totalBudget]);

      return Object.fromEntries(queryParamsArray);
    },
  },
  watch: {
    queryParams() {
      this.$router.push({ query: this.queryParams });
    },
  },
  created() {
    this.setQueryParams();
    this.startProductSelection();
  },
};
</script>

<style>
.inputForm {
  align-self: center;
  margin-bottom: 10px;
  padding: 5px 10px;
  border-radius: 5px;
}
.inputForm:focus {
  border-color: black;
}
</style>

<style scoped>
.productList {
  min-width: 480px;
  display: flex;
  flex-direction: column;
  align-items: center;
  margin: 20px;
}

h1 {
  margin: 20px 0 30px 0;
}
h3 {
  margin: 10px;
  align-self: center;
}
.productInput {
  min-width: 480px;
  display: flex;
  flex-direction: column;
  align-items: flex-start;
}
.inputForm {
  align-self: center;
  margin-bottom: 10px;
  padding: 5px 10px;
  border-radius: 5px;
}
.inputForm:focus {
  border-color: black;
}
.course {
  margin: 15px;
}

.bounce-enter-active {
  animation: bounce-in 0.5s;
}

.bounce-leave-active {
  animation: bounce-in 0.5s reverse;
}

@keyframes bounce-in {
  0% {
    transform: scale(0);
  }
  100% {
    transform: scale(1);
  }
}

.btn {
  margin: 20px;
  align-self: center;
}
.btn:hover {
  color: black !important;
  background-color: rgb(217, 154, 36) !important;
  border-color: rgb(217, 154, 36) !important;
}
</style>
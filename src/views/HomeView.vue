// Форма добавления новой статьи доходов\расходов
<template>
  <div class="home">
    <img alt="Vue logo" src="../assets/logo.png" />
    <HelloWorld msg="Приложения учет доходов" />
    <FormCost @addCostInTable="addCostInTable" />
    <TableCost :itemCost="PaymentsList"></TableCost>
  </div>
</template>

<script>
// @ is an alias to /src
import HelloWorld from "@/components/HelloWorld.vue";
import FormCost from "@/components/FormCost.vue";
import TableCost from "@/components/TableCost.vue";

export default {
  name: "HomeView",
  components: {
    HelloWorld,
    FormCost,
    TableCost,
  },
  data() {
    return { PaymentsList: [] };
  },

  methods: {
    getData() {
      return [
        { numberId: "", date: "28.04.2022", category: "sport", amount: 3000 },
        {
          numberId: "",
          date: "27.04.2022",
          category: "transport",
          amount: 5000,
        },
        { numberId: "", date: "24.04.2022", category: "leiser", amount: 2000 },
      ];
    },
    addCostInTable(data) {
      // this.PaymentsList = [...this.PaymentsList, data];
      this.PaymentsList.push(data);
      console.log(data);
    },
  },
  created() {
    this.PaymentsList = this.getData();
  },
};
</script>

<style>
img {
  width: 50px;
  height: 50px;
}
</style>
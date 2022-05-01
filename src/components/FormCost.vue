<template>
  <div class="formCostWrp">
    <button class="btnAddNewCost" @click="visible = !visible">
      Add new cost
    </button>
    <div class="formCost" v-show="visible">
      <input type="text" placeholder="Date" v-model="date" />
      <input type="text" placeholder="Category" v-model="category" />
      <input type="text" placeholder="Amount" v-model="amount" />
      <div class="btnSave">
        <button @click="addCostInTable">Save</button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "FormCost",
  data() {
    return {
      numberId: "",
      date: "",
      category: "",
      amount: "",
      visible: false,
      dateIntl: "",
    };
  },
  computed: {
    // getCurrenDate() {
    //   let today = new Date();
    //   let d = today.getDate();
    //   let m = today.getMonth() + 1;
    //   let y = today.getFullYear();
    //   return `${d}.${m}.${y}`;
    // },
  },

  methods: {
    addCostInTable() {
      // const data = {
      //   numberId: +this.numberId++,
      //   date: this.date || this.getCurrenDate,
      //   category: this.category,
      //   amount: +this.amount,
      // };
      const data = {
        numberId: +this.numberId++,
        date: this.dateIntl,
      };

      // console.log(data);
      this.$emit("addCostInTable", data);
    },
  },
  created() {
    this.dateIntl = new Intl.DateTimeFormat("ru").format(new Date());
    console.log(`${this.dateIntl} это dateIntl`);
  },
};
</script>



<style>
.formCost {
  margin: 20px 0 0 0;
}
input {
  height: 30px;
  margin: 20px 0 0 20px;
}
.btnSave {
  margin: 20px 0 0 0;
}
.btnAddNewCost {
  text-transform: uppercase;
  height: 40px;
  background-color: mediumseagreen;
}
</style>
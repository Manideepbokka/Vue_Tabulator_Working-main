<template>
  <div class="hello">
    <vue-tabulator v-model="dados" :options="options" />
  </div>
</template>

<script>
import axios from 'axios';
import Vue from "vue";
import vueTabulator from "vue-tabulator";

Vue.use(vueTabulator, { name: "vue-tabulator" });

export default {
  name: "HelloWorld",
  data() {
    return {
      dados: [],
      options: {
        selectable: 1,
        columns: [
          {
            title: "MayoClinic Urls",
            frozen: true,
            columns: [
              {
                title: "S.NO",
                field: "id",
                sorter: "string",
                width: 100,
              },
              {
                title: "URLS",
                field: "url",
                sorter: "string",
                width: 400,
              },
            ],
          },

        ],
      },
    };
  },
  created() {
    axios.get(`http://127.0.0.1:8000`,{headers: {'Access-Control-Allow-Origin': '*'}})
    .then(response => {
   
      this.dados = response.data
    })
    .catch(e => {
      this.errors.push(e)
    })
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="scss" scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}

.tabulator {
  height: 400px;
}
.tabulator-tableHolder::-webkit-scrollbar {
  -webkit-appearance: none;
  width: 6px;
  height: 6px;
}
.tabulator-tableHolder::-webkit-scrollbar-thumb {
  border-radius: 4px;
  background-color: #C4C4C4;
}
</style>

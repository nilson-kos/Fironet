<template>
  <div id="app">
    <table>
      <tr>
        <th>Image</th>
        <th>FullName</th>
        <th>NAME</th>
        <th>PRICE</th>
        <th>SUPPLY</th>
      </tr>
      <tr v-for="index of info">
        <td>
          <img :src="'https://www.cryptocompare.com/' + index.CoinInfo.ImageUrl" alt="">
        </td>
        <td>
          {{ index.CoinInfo.FullName }}
        </td>
        <td>
          {{ index.CoinInfo.Name }}
        </td>
        <td>
          {{ index.RAW.USD.PRICE }}
        </td>
        <td>
          {{ index.RAW.USD.SUPPLY }}
        </td>
      </tr>
    </table>
  </div>
</template>

<script>
  import axios from 'axios';

  export default {
    name: 'app',
    data() {
      return {
        info: [],
      };
    },
    methods: {
      test() {
        axios.get('https://min-api.cryptocompare.com/data/top/mktcapfull?limit=20&tsym=USD')
                .then(response => {
                  this.info = response.data.Data
                  this.info.sort(function (a, b) {
                    return b.RAW.USD.PRICE - a.RAW.USD.PRICE;
                  });
                  console.log('done',this.info);
                });
      }
    },
    created() {
        this.test();
        setInterval(() => this.test(), 300000);
    },
  }
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 10px;
}

img {
  width: 40px;
}

table {
  margin-left: auto;
  margin-right: auto;
}

th, td {
  border: 1px solid #ddd;
  padding: 8px;
  text-transform: uppercase;
}

tr:hover {background-color: #f5f5f5;}


th {
  padding-top: 12px;
  padding-bottom: 12px;

  background-color: #4CAF50;
  color: white;
}
</style>

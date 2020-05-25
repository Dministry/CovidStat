<template>
  <div id="app">
    <Navbar class="mb-2" />
    <h1>COVID-19 STATISTICS</h1>
    <hr />
    <div class="container">
      <div class="row">
        <div class="col-4">
          <h2>COVID-19 GLOBAL</h2>
          <ul>
            <li class="global">New Confirmed: {{ cases.NewConfirmed }}</li>
            <li class="global">Total Confirmed: {{ cases.TotalConfirmed }}</li>
            <li class="global">Total Deaths: {{ cases.TotalDeaths }}</li>
            <li class="global">Total Recovered: {{ cases.TotalRecovered }}</li>
            <!-- <button href="" @click="handleClick()">Click me</button> -->
          </ul>
        </div>
        <!-- <div class="col-4" v-for="(value, index) in base" :key="index">
          {{ value }}
        </div> -->
        <div class="col-8">
          <h2>COVID-19 NIGERIA</h2>
          <div class="flex-display">
            <div class="card">
              <div class="header">
                <font-awesome-icon icon="viruses" />
                <h1>{{ confirmed }}</h1>
              </div>

              <div class="container">
                <p>Total Confirmed</p>
              </div>
            </div>
            <div class="card">
              <div class="header2">
                <font-awesome-icon icon="viruses" />
                <h1>{{ active }}</h1>
              </div>

              <div class="container">
                <p>Total Active</p>
              </div>
            </div>
            <div class="card">
              <div class="header3">
                <font-awesome-icon icon="viruses" />
                <h1>{{ recovered }}</h1>
              </div>

              <div class="container">
                <p>Total Recovered</p>
              </div>
            </div>
            <div class="card">
              <div class="header4">
                <font-awesome-icon icon="viruses" />
                <h1>{{ death }}</h1>
              </div>

              <div class="container">
                <p>Total Death</p>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
    <div id="option">
      <h2>Corona Virus Cases Worldwide</h2>
      <select id="" v-model="country">
        <option
          v-for="(county, index) in countries"
          :key="index"
          :value="county.Slug"
        >
          {{ county.Country }}
        </option> </select
      ><br />
      <button @click="getCountry" class="btn btn-primary">
        Get Covid-19 Data
      </button>
      <h1>Total Confirmed Cases: {{ confirmedx }}</h1>
      <h1>Total Recovered Cases {{ recoveredx }}</h1>
      <h1>Total Deaths Cases: {{ deathx }}</h1>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src
import axios from "axios";
import Navbar from "../components/Navbar";
export default {
  name: "Home",
  components: {
    Navbar
  },
  data() {
    return {
      cases: {},
      base: {},
      countries: {},
      country: "",
      confirmed: "",
      death: "",
      recovered: "",
      active: "",
      date: "",
      confirmedx: "",
      deathx: "",
      recoveredx: "",
      activex: "",
      datex: "",
      url_base: "https://api.covid19api.com/country/"
    };
  },
  methods: {
    getCountry: function() {
      axios.get(`${this.url_base}${this.country}`).then(res => {
        var indexx = res.data.length - 1;
        // this.base = res.data.length - 1;
        this.confirmedx = res.data[indexx].Confirmed;
        this.deathx = res.data[indexx].Deaths;
        this.recoveredx = res.data[indexx].Recovered;
        this.activex = res.data[indexx].Active;
        this.datex = res.data[indexx].Date;
      });
    }
  },
  created() {
    axios.get("https://api.covid19api.com/summary").then(res => {
      this.cases = res.data.Global;
    });
    axios.get("https://api.covid19api.com/country/nigeria").then(res => {
      var index = res.data.length - 1;
      // this.base = res.data.length - 1;
      this.confirmed = res.data[index].Confirmed;
      this.death = res.data[index].Deaths;
      this.recovered = res.data[index].Recovered;
      this.active = res.data[index].Active;
      this.date = res.data[index].Date;
      console.log(this.base);
    });
    axios.get("https://api.covid19api.com/countries").then(res => {
      this.countries = res.data;
    });
    axios.get(`${this.url_base}${this.country}`).then(res => {
      var indexx = res.data.length - 1;
      // this.base = res.data.length - 1;
      this.confirmedx = res.data[indexx].Confirmed;
      this.deathx = res.data[indexx].Deaths;
      this.recoveredx = res.data[indexx].Recovered;
      this.activex = res.data[indexx].Active;
      this.datex = res.data[indexx].Date;
    });
  }
};
</script>

<style scoped>
* {
  font-family: Arial, Helvetica, sans-serif;
}
.global {
  background-color: #ff0000;
  border-radius: 8px;
  line-height: 4;
  background-image: linear-gradient(#971010a9, #c0bfbf8e);
  /* border: 1px solid red; */
}
ul > li {
  list-style: none;
  box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2), 0 6px 20px 0 rgba(0, 0, 0, 0.19);
  color: white;
  font-family: Arial, Helvetica, sans-serif;
  font-weight: 600;
}
.flex-display {
  display: flex;
}
div.card {
  width: 250px;
  box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2), 0 6px 20px 0 rgba(0, 0, 0, 0.19);
  text-align: center;
  margin-right: 2em;
  border-radius: 6px;
}

div.header {
  background-color: #2196f3;
  color: white;
  padding: 10px;
  font-size: 40px;
  border-radius: 6px;
}
div.header2 {
  background-color: #4caf50;
  color: white;
  padding: 10px;
  font-size: 40px;
  border-radius: 6px;
}
div.header3 {
  background-color: #ff9800;
  color: white;
  padding: 10px;
  font-size: 40px;
  border-radius: 6px;
}
div.header4 {
  background-color: #f44336;
  color: white;
  padding: 10px;
  font-size: 40px;
  border-radius: 6px;
}

div.container {
  padding: 10px;
}
</style>

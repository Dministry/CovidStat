<template>
  <div id="app">
    <Navbar class="mb-2" />
    <h1>COVID-19 STATISTICS</h1>
    <hr />
    <div class="container">
      <div class="row" id="container2">
        <div class="col-12 mx-2 my-2 justify-content-center col-lg-3 col-xs-3">
          <h4>GLOBAL</h4>
          <ul id="globe">
            <li class="global">
              New Confirmed: <br />{{ cases.NewConfirmed }}
            </li>
            <li class="global">
              Total Confirmed: <br />{{ cases.TotalConfirmed }}
            </li>
            <li class="global">Total Deaths: <br />{{ cases.TotalDeaths }}</li>
            <li class="global">
              Total Recovered: <br />{{ cases.TotalRecovered }}
            </li>
            <!-- <button href="" @click="handleClick()">Click me</button> -->
          </ul>
        </div>
        <!-- <div class="col-4" v-for="(value, index) in base" :key="index">
          {{ value }}
        </div> -->
        <div class="col-12 mx-2 my-2 justify-content-center col-lg-8 col-xs-8">
          <h4>NIGERIA</h4>
          <div id="card">
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
      <table id="container" class="table table-light">
        <h2>Corona Virus Cases Worldwide</h2>
        <label for="country">Select Country below:</label>
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
        <thead>
          <tr>
            <th scope="col">Confirmed Cases</th>
            <th scope="col">Recovered Cases</th>
            <th scope="col">Death Cases</th>
          </tr>
        </thead>
        <tbody>
          <tr>
            <td class="tabd">{{ confirmedx }}</td>
            <td class="tabd">{{ recoveredx }}</td>
            <td class="tabd">{{ deathx }}</td>
          </tr>
        </tbody>
      </table>
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
  box-sizing: border-box;
}
#globe {
  background-color: #0d9636a9;
  border-radius: 8px;
  padding-left: 0;
}
ul > li {
  list-style: none;
  color: rgb(247, 244, 244);
  font-family: Arial, Helvetica, sans-serif;
  font-weight: 500;
}
div.card {
  max-width: 48vmax;
  min-width: 22vmin;
  box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2), 0 6px 20px 0 rgba(0, 0, 0, 0.19);
  margin: 0.5em 0.2em;
  border-radius: 6px;
  display: flex;
}
#card {
  display: flex;
  flex-wrap: wrap;
  margin-top: 0.5em;
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
html {
  font-family: Arial, Helvetica, sans-serif;
}
table {
  background-image: linear-gradient(
    rgba(246, 247, 248, 0.267),
    rgba(174, 235, 182, 0.164)
  );
  display: flex;
  align-items: center;
  flex-direction: column;
  justify-content: center;
  padding-top: 16px;
  transition: all 0.3s ease-in;

  @media (max-width: 512px) {
    padding: 320px;
    transition: all 0.3s ease-in;
  }

  @media (max-width: 360px) {
    padding: 16px;
    transition: all 0.3s ease-in;
  }
}
#container {
  max-width: 1080px;
  margin: 0 auto;
  background-color: rgba(87, 172, 211, 0.5);
  padding: 64px;
  box-shadow: 2px 2px 50px #111;
  border-radius: 10px;
  transition: all 0.3s ease-in;
  @media (max-width: 512px) {
    padding: 32px;
    transition: all 0.3s ease-in;
  }
  @media (max-width: 360px) {
    padding: 16px;
    transition: all 0.3s ease-in;
  }
}
#container2 {
  max-width: 1080px;
  margin: 0 auto;
  background-color: rgba(87, 172, 211, 0.5);
  padding: 64px;
  box-shadow: 2px 2px 50px #111;
  border-radius: 10px;
  transition: all 0.3s ease-in;
  @media (max-width: 512px) {
    padding: 32px;
    transition: all 0.3s ease-in;
  }
  @media (max-width: 360px) {
    padding: 16px;
    transition: all 0.3s ease-in;
  }
}
h1 {
  text-align: center;
  color: rgb(143, 27, 37);
  margin: 0 0 16px 0;
  line-height: 2;
  font-size: xx-large;
}
.tabd {
  padding-right: 6em;
}
h4 {
  font-weight: 600;
}
</style>

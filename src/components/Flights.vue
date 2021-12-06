<template>
  <div class="m-2 p-2">
    <b-tabs
      active-nav-item-class="font-weight-bold text-uppercase text-dark"
      content-class="mt-3 font-weight-bold"
    >
      <b-tab title="Flights" class="text-dark" active>
        <div class="row">
          <div class="col-md-8">
            <div class="row g-1" id="fight-search">
              <div class="col-md-3 shadow">
                <b-card
                  class="text-center rounded-0"
                  id="fight-search-card"
                  v-b-modal.modal-center1
                >
                  <b-card-text>
                    <p>Leaving From</p>
                    <h1>{{ leavingFrom }}</h1>
                    <h3>{{ leavingFromCity }}</h3>
                  </b-card-text>
                </b-card>
              </div>
              <div class="col-md-3 shadow">
                <b-card
                  class="text-center rounded-0"
                  id="fight-search-card"
                  v-b-modal.modal-center1
                >
                  <b-card-text>
                    <p>Going To</p>
                    <h1>{{ goingTo }}</h1>
                    <h3>{{ goingToCity }}</h3>
                  </b-card-text>
                </b-card>
              </div>

              <div class="col-md-3 border-3 shadow">
                <b-card
                  class="text-center rounded-0"
                  id="fight-search-card"
                  v-b-modal.modal-center
                >
                  <b-card-text
                    >Departing on
                    <h3>{{ dates.in }}</h3>
                  </b-card-text>
                  <hr />
                  <b-card-text
                    >Returning on
                    <h3>{{ dates.out }}</h3>
                  </b-card-text>
                </b-card>

                <div>
                  <b-modal id="modal-center" centered title="Select Date">
                    <p class="my-4">
                      <HotelDatePicker
                        @check-in-changed="checkInDate"
                        @check-out-changed="checkOutDate"
                        format="YYYY-MM-DD"
                      >
                      </HotelDatePicker>
                    </p>
                  </b-modal>
                </div>
              </div>
              <div class="col-md-3 shadow">
                <button
                  size="lg"
                  class="btn btn-grad w-100 h-100 rounded-0"
                  @click="searchFlights()"
                >
                  <h1>
                    <font-awesome-icon icon="plane" />
                  </h1>
                  <h2>Search Flight</h2>
                </button>
              </div>
            </div>

            <div class="row mt-3 g-1">
              <div class="col-md-3 shadow">
                <b-card
                  class="text-center rounded-0 w-100 h-100"
                  border-variant="light"
                  text-variant="white"
                  id="flight-card"
                >
                  <b-card-text>
                    <h1>
                      <font-awesome-icon icon="list" />
                    </h1>
                    <h2>Manage Booking</h2>
                  </b-card-text>
                </b-card>
              </div>
              <div class="col-md-3 shadow">
                <b-card
                  class="text-center rounded-0 w-100 h-100"
                  border-variant="light"
                  text-variant="white"
                  id="flight-card"
                >
                  <b-card-text>
                    <h1>
                      <font-awesome-icon icon="ticket-alt" />
                    </h1>
                    <h2>Check in</h2>
                  </b-card-text>
                </b-card>
              </div>
              <div class="col-md-3 shadow">
                <b-card
                  class="text-center rounded-0 w-100 h-100"
                  border-variant="light"
                  text-variant="white"
                  id="flight-card"
                >
                  <b-card-text>
                    <h1>
                      <font-awesome-icon icon="exchange-alt" />
                    </h1>
                    <h2>Rebook and Refund</h2>
                  </b-card-text>
                </b-card>
              </div>
              <div class="col-md-3 shadow">
                <b-card
                  class="text-center rounded-0 w-100 h-100"
                  border-variant="light"
                  text-variant="white"
                  id="flight-card"
                >
                  <b-card-text>
                    <h1>
                      <font-awesome-icon icon="exclamation-triangle" />
                    </h1>
                    <h2>Covid-19 Update</h2>
                  </b-card-text>
                </b-card>
              </div>
            </div>
          </div>
          <div class="col-md-4">
            <div class="h-100 w-auto">
              <img
                src="https://www.cathaypacific.com/content/dam/focal-point/digital-library/destinations/cebu-ceb/CEB_006Y19.renditionimage.900.450.jpg"
                alt=""
                class="img-fluid h-100 w-100"
              />
            </div>
          </div>
        </div>
      </b-tab>
    </b-tabs>
    <div>
      <b-modal id="modal-center1" centered title="Select Place">
        <div>
          <b-form-input
            v-model="searchLeavingFrom"
            placeholder="Enter departing on"
            @input="searchingLeavingFrom()"
          ></b-form-input>
        </div>
        <div
          class="from-list shadow"
          v-if="flightFromStatus"
          id="flightFromList"
        >
          <tr
            class="border-1 p-2"
            v-for="(flight, index) in flight_code"
            :key="index"
            style="cursor: pointer; background-color: whitesmoke"
          >
            <td
              class="p-1 m-1"
              scope="col"
              @click="setFlightFrom(flight[2], flight[1])"
            >
              <b> {{ flight[1] }}</b> ,<b>{{ flight[2] }}</b> ,
              {{ flight[0] }}
            </td>
          </tr>
        </div>
        <br />
        <div>
          <b-form-input
            v-model="searchGoingTo"
            placeholder="Enter returning on"
            @input="searchingGoingTo()"
          ></b-form-input>
        </div>
        <div class="from-list" v-if="flightToStatus" id="flightToList">
          <tr
            v-for="(flight, index) in flight_code"
            :key="index"
            style="cursor: pointer; background-color: whitesmoke"
          >
            <td
              class="p-1 m-1"
              scope="col"
              @click="setFlightTo(flight[2], flight[1])"
            >
              <b> {{ flight[1] }}</b> ,<b>{{ flight[2] }}</b> ,
              {{ flight[0] }}
            </td>
          </tr>
        </div>
      </b-modal>
    </div>

    <div class="mt-3">
      <div class="row">
        <div class="col-md-4"></div>
        <div class="col-md-4"></div>
        <div class="col-md-4"></div>
      </div>
    </div>

    <div class="mt-3">
      <div>
        <li class="border-1" style="list-style-type: none">
          <b-card class="card-class text-white" id="flightList">
            <b-row>
              <b-col style="text-align: center">
                <h2>Departure Time</h2>
              </b-col>
              <b-col style="text-align: center">
                <h2>Duration</h2>
              </b-col>
              <b-col style="text-align: center">
                <h2>Arrival Time</h2>
              </b-col>
              <b-col style="text-align: center">
                <h2>Price</h2>
              </b-col>
            </b-row>
          </b-card>
        </li>
        <li
          class="border-1 mt-1 bg-gradient"
          style="list-style-type: none"
          v-for="flightData of flightsData"
          :key="flightData.index"
        >
          <b-card class="card-class text-white" id="flightList">
            <b-row>
              <b-col style="text-align: center">
                <h2>{{ flightData.departureTime }}</h2>
                <h3>{{ flightData.originCode }}</h3>
              </b-col>
              <b-col style="text-align: center">
                <h1>
                  <font-awesome-icon icon="plane" />
                </h1>
                <h3>{{ flightData.durationTime }}</h3>
              </b-col>
              <b-col style="text-align: center">
                <h2>{{ flightData.arivalTime }}</h2>
                <h3>{{ flightData.destinationCode }}</h3>
              </b-col>
              <b-col style="text-align: center">
                <h1></h1>
                <h2>{{ flightData.price }} BDT</h2>
              </b-col>
            </b-row>
          </b-card>
        </li>
      </div>
    </div>
  </div>
</template>

<script>
import HotelDatePicker from "vue-hotel-datepicker";
import "vue-hotel-datepicker/dist/vueHotelDatepicker.css";
import { autocomplete } from "air-port-codes-node";
import axios from "axios";

export default {
  components: {
    HotelDatePicker,
  },
  data() {
    return {
      flightFromStatus: false,
      flightToStatus: false,
      searchLeavingFrom: "",
      searchGoingTo: "",
      leavingFrom: "",
      goingTo: "",
      leavingFromCity: "",
      goingToCity: "",
      departingOn: "",
      returningOn: "",
      flight_code: [],
      dates: {
        in: new Date().toISOString().slice(0, 10),
        out: new Date().toISOString().slice(0, 10),
      },
      apca: autocomplete({
        key: "763c531c39",
        secret: "a6741e771d9252d", // Your API Secret Key: use this if you are not connecting from a web server
        limit: 5,
      }),
      flightsData: [],
    };
  },
  methods: {
    checkInDate(val) {
      this.dates.in = val.toISOString().slice(0, 10);
    },
    checkOutDate(val) {
      this.dates.out = val.toISOString().slice(0, 10);
    },
    searchingLeavingFrom() {
      this.flightFromStatus = true;
      this.apca.request(this.searchLeavingFrom);
      this.apca.onSuccess = (data) => {
        if (data.airports.length > 0 && this.searchLeavingFrom.length > 0) {
          document.getElementById("flightFromList").style.display = "block";
          this.flight_code = [];
          for (let i = 0; i < data.airports.length; i++) {
            this.flight_code[i] = [
              data.airports[i].name,
              data.airports[i].city,
              data.airports[i].iata,
            ];
          }
        }
      };
      this.apca.onError = (data) => {
        console.log("onError", data.message);
      };
    },
    searchingGoingTo() {
      this.flightToStatus = true;
      this.apca.request(this.searchGoingTo);
      this.apca.onSuccess = (data) => {
        if (data.airports.length > 0 && this.searchGoingTo.length > 0) {
          document.getElementById("flightToList").style.display = "block";
          this.flight_code = [];
          for (let i = 0; i < data.airports.length; i++) {
            this.flight_code[i] = [
              data.airports[i].name,
              data.airports[i].city,
              data.airports[i].iata,
            ];
          }
        }
      };
      this.apca.onError = (data) => {
        console.log("onError", data.message);
      };
    },
    setFlightFrom(iata, city) {
      this.leavingFrom = iata;
      this.leavingFromCity = city;
      document.getElementById("flightFromList").style.display = "none";
    },
    setFlightTo(iata, city) {
      this.goingTo = iata;
      this.goingToCity = city;
      document.getElementById("flightToList").style.display = "none";
    },
    searchFlights() {
      var url =
        "https://api.sharetrip.net/api/v1/flight/search?tripType=Return&adult=1&child=0&infant=0&class=Economy&origin=" +
        this.leavingFrom +
        "&destination=" +
        this.goingTo +
        "&depart=" +
        this.dates.in +
        "&depart=" +
        this.dates.out;
      console.log(url);
      axios
        .get(url)
        .then((response) => {
          response = JSON.stringify(response);
          response = JSON.parse(response);
          let counterValue = 0;
          let allFlightsData = [];
          let flightPrices = [
            9876, 2342, 1947, 10000, 45000, 5000, 3333, 7654, 12345, 6567,
          ];
          const flightsLength = response.data.response.flights.length;
          try {
            for (let i = 0; i < flightsLength; i++) {
              const originCity =
                response.data.response.flights[i].flight[0].originName.city;
              const originAirport =
                response.data.response.flights[i].flight[0].originName.airport;
              const destinationCity =
                response.data.response.flights[i].flight[0].destinationName
                  .city;
              const originCode =
                response.data.response.flights[i].flight[0].originName.code;
              const destinationAirport =
                response.data.response.flights[i].flight[0].destinationName
                  .airport;
              const destinationCode =
                response.data.response.flights[i].flight[0].destinationName
                  .code;
              const arivalTime =
                response.data.response.flights[i].flight[0].arrivalDateTime
                  .time;
              const departureTime =
                response.data.response.flights[i].flight[0].departureDateTime
                  .time;
              const durationTime =
                response.data.response.flights[i].flight[0].duration;
              const flightPrice = response.data.response.flights[i].price;
              const logo = response.data.response.flights[i].flight[0].logo;
              const eachFlightData = {
                index: i,
                originCity: originCity,
                destinationCity: destinationCity,
                originCode: originCode,
                destinationCode: destinationCode,
                arivalTime: arivalTime,
                departureTime: departureTime,
                originAirport: originAirport,
                destinationAirport: destinationAirport,
                price: flightPrice,
                durationTime: durationTime,
                logo: logo,
              };
              allFlightsData.push(eachFlightData);
              counterValue++;
            }
          } catch (error) {
            console.log("Error" + error.message);
          }
          this.flightsData = allFlightsData;
          console.log(this.flightsData);
        })
        .catch((e) => {
          this.errors.push(e);
        });
    },
    getWeather(val) {
      const options = {
        method: "GET",
        url: "https://weatherapi-com.p.rapidapi.com/forecast.json",
        qs: { q: `${val}`, days: "3" },
        headers: {
          "x-rapidapi-host": "weatherapi-com.p.rapidapi.com",
          "x-rapidapi-key":
            "af8a4d5d3emshe34311a0dfd42e3p1d160bjsn7ba404c8d59d",
          useQueryString: true,
        },
      };
    },
  },
};
</script>

<style scoped>
#fight-search {
  min-height: 20vh;
}
#fight-search-card {
  min-height: 100%;
  background: linear-gradient(whitesmoke, rgba(245, 245, 245, 0.904)),
    linear-gradient(to right, #005d63, #6cc2c9d7);
  border: 5px solid transparent;
  background-repeat: no-repeat;
  background-origin: padding-box, border-box;
}
#flight-card {
  background-image: linear-gradient(
    to right,
    #005d63 0%,
    #005c63af 51%,
    #005d63 100%
  );
}

#flight-card {
  text-align: center;
  text-transform: uppercase;
  transition: 0.5s;
  background-size: 200% auto;
  color: white;
  box-shadow: 0 0 20px rgba(238, 238, 238, 0.603);
  border-radius: 10px;
  display: block;
}

#flight-card:hover {
  background-position: right center;
  color: #fff;
  text-decoration: none;
}

.btn-grad {
  background-image: linear-gradient(
    to right,
    #005d63 0%,
    #005c63af 51%,
    #005d63 100%
  );
}
.btn-grad {
  text-align: center;
  text-transform: uppercase;
  transition: 0.5s;
  background-size: 200% auto;
  color: white;
  box-shadow: 0 0 20px #eee;
  border-radius: 10px;
  display: block;
}

.btn-grad:hover {
  background-position: right center;
  color: #fff;
  text-decoration: none;
}
#flightList {
  background-image: linear-gradient(
    to right,
    #005d63 0%,
    #005c63af 51%,
    #005d63 100%
  );
}
</style>

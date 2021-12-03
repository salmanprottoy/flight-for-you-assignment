<template>
  <div class="m-2 p-2">
    <b-tabs
      active-nav-item-class="font-weight-bold text-uppercase text-dark"
      content-class="mt-3 font-weight-bold"
    >
      <b-tab title="Flights" class="text-dark" active>
        <div class="row g-1" id="fight-search">
          <div class="col-md-3 shadow">
            <b-card class="text-center rounded-0" id="fight-search-card">
              <b-card-text>
                <p>Leaving From</p>
                <h1>CDS</h1>
                <h3>dhaka</h3>
              </b-card-text>
            </b-card>
          </div>
          <div class="col-md-3 shadow">
            <b-card class="text-center rounded-0" id="fight-search-card">
              <b-card-text>
                <p>Going To</p>
                <h1>CDS</h1>
                <h3>dhaka</h3>
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
            <button size="lg" class="btn btn-grad w-100 h-100 rounded-0">
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
      </b-tab>
    </b-tabs>
  </div>
</template>

<script>
import HotelDatePicker from "vue-hotel-datepicker";
import "vue-hotel-datepicker/dist/vueHotelDatepicker.css";

export default {
  components: {
    HotelDatePicker,
  },
  data() {
    return {
      leavingFrom: "",
      goingTo: "",
      departingOn: "",
      returningOn: "",
      dates: {
        in: new Date().toISOString().slice(0, 10),
        out: new Date().toISOString().slice(0, 10),
      },
    };
  },
  methods: {
    checkInDate(val) {
      this.dates.in = val.toISOString().slice(0, 10);
    },
    checkOutDate(val) {
      this.dates.out = val.toISOString().slice(0, 10);
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
</style>

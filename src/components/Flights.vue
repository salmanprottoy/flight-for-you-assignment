<template>
  <div class="m-2 p-2">
    <b-tabs content-class="mt-3 font-weight-bold">
      <b-tab title="Flights" class="text-dark" active>
        <div class="row" id="fight-search">
          <div class="col-md-3">
            <b-card class="text-center" id="fight-search-card">
              <b-card-text>
                <p>Leaving From</p>
                <h1>CDS</h1>
                <h3>dhaka</h3>
              </b-card-text>
            </b-card>
          </div>
          <div class="col-md-3">
            <b-card class="text-center" id="fight-search-card">
              <b-card-text>
                <p>Going To</p>
                <h1>CDS</h1>
                <h3>dhaka</h3>
              </b-card-text>
            </b-card>
          </div>
          <div class="col-md-3">
            <b-card class="text-center" id="fight-search-card">
              <b-card-text
                >Departing on
                <h3>2021-10-10</h3>
              </b-card-text>
              <hr />
              <b-card-text
                >Returning on
                <h3>2021-10-10</h3>
              </b-card-text>
            </b-card>
          </div>
          <div class="col-md-3">
            <b-button variant="success" size="lg" class="w-100 h-100">
              <h2>Search Flight</h2>
            </b-button>
          </div>
        </div>
      </b-tab>
    </b-tabs>
  </div>
</template>

<script>
export default {
  data() {
    return {
      leavingFrom: "",
      goingTo: "",
      departingOn: "",
      returningOn: "",
    };
  },
};
</script>

<style scoped>
#fight-search {
  min-height: 20vh;
}
#fight-search-card {
  min-height: 100%;
}
</style>

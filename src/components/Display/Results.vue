<script>
import Row from "./Row.vue";
export default {
  name: "Results",
  props: ["flightData"],
  components: {
    Row,
  },
  methods: {
    getFresh(flightOffer) {
      let unifiedData = [];
      let ptr = 0;

      let price = flightOffer.price;
      let seat = flightOffer.seat;
      let clas = flightOffer.class;
      let fareBasis = flightOffer.fareBasis;
      let itineraries = flightOffer.itineraries;

      for (let j = 0; j < seat.length; j++) {
        for (let k = 0; k < seat[j].length; k++) {
          let segments = itineraries[j].segments;
          let duration = itineraries[j].duration;
          for (let l = 0; l < segments.length; l++) {
            let departurePlace = segments[l].departure.iataCode;
            let departureTime = segments[l].departure.at;
            let arrivalPlace = segments[l].arrival.iataCode;
            let arrivalTime = segments[l].arrival.at;
            let marketingCarrier = segments[l].marketingCarrier;
            let carrierCode = segments[l].carrierCode;
            let flightNumber = segments[l].flightNumber;
            let aircraft = segments[l].aircraft;
            
            unifiedData[ptr++] = {
              price: price,
              seat: seat[j][k],
              class: clas[j][k],
              fareBasis: fareBasis[j][k],
              duration: duration,
              departurePlace: departurePlace,
              departureTime: departureTime,
              arrivalPlace: arrivalPlace,
              arrivalTime: arrivalTime,
              marketingCarrier: marketingCarrier,
              carrierCode: carrierCode,
              flightNumber: flightNumber,
              aircraft: aircraft,
            };
          }
        }
      }

      return unifiedData;
    },
  },
};
</script>

<template>
  <div v-for="(flightOffer, x) in flightData" :key="x">
    <div v-for="(fresh, y) in getFresh(flightOffer)" :key="y">
        {{ fresh }}
        <br><br>
    </div>

    <hr />
  </div>
</template>
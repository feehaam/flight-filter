<script>
import Row from "./Row.vue";
export default {
  name: "Results",
  props: [
    "flightData",
    "tripType",
    "inputFrom",
    "inputTo",
    "inputStartDate",
    "inputReturnDate",
    "inputStartTime",
    "inputReturnTime",
  ],
  components: {
    Row,
  },
  methods: {
    getFresh(flightOffer) {
      if(this.tripType == 'multi') return;
      let unifiedData = [];
      let ptr = 0;
      // Extra space for round trip checkings
      let allData = [];
      let adPtr = 0;

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

            let canAdd = true;
            if ((this.inputFrom != null) & (this.inputFrom.length > 0)) {
              if (!departurePlace.includes(this.inputFrom)) canAdd = false;
            }
            if ((this.inputTo != null) & (this.inputTo.length > 0)) {
              if (!arrivalPlace.includes(this.inputTo)) canAdd = false;
            }
            if (
              (this.inputStartDate != null) &
              (this.inputStartDate.length > 0)
            ) {
              if (!departureTime.includes(this.inputStartDate)) canAdd = false;
            }
            if (this.inputStartTime != null && this.inputStartTime.length > 0) {
              let depTime = departureTime.substring(
                11,
                departureTime.length - 6
              );
              let inDepTime = this.inputStartTime.substring(0, 2);
              if (depTime !== inDepTime) canAdd = false;
            }

            let flight = {
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
            if (canAdd)
              unifiedData[ptr++] = flight;
            allData[adPtr++] = flight;
          }
        }
      }

      if (this.tripType === "round") {
        let roundOnlyFlights = [];
        let rrPtr = 0;
        for (let i = 0; i < unifiedData.length; i++) {
          let ac = unifiedData[i].aircraft;
          for(let j=0; j<allData.length; j++){
            if(allData[j].aircraft === ac && allData[j].departurePlace === this.inputTo && allData[j].arrivalPlace === this.inputFrom){
              roundOnlyFlights[rrPtr++] = unifiedData[i];
              roundOnlyFlights[rrPtr++] = allData[j];
              break;
            }
          }
        }
        return roundOnlyFlights;
      }

      return unifiedData;
    },
  },
};
</script>

<template>
  {{ tripType === 'round' ? "Please select one way trip!" : "" }}
  {{ tripType === 'multi' ? "Please select one way trip!" : "" }}

  <div class="mycont border rounded-md shadow-md p-2 mb-5 py-6 bg-gray-200">
    <div class="myitem hover:bg-gray-300 hover:cursor-grab">
        FLIGHT
    </div>
    <div class="myitem hover:bg-gray-300 hover:cursor-grab">
        AC.
    </div>
    <div class="myitem hover:bg-gray-300 hover:cursor-grab">
        CLASS
    </div>
    <div class="myitem hover:bg-gray-300 hover:cursor-grab">
        FARE B.
    </div>
    <div class="myitem hover:bg-gray-300 hover:cursor-grab">
        ROUTE
    </div>
    <div class="myitem hover:bg-gray-300 hover:cursor-grab">
        DEPARTURE TIME
    </div>
    <div class="myitem hover:bg-gray-300 hover:cursor-grab">
        ARRIVAL TIME
    </div>
    <div class="myitem hover:bg-gray-300 hover:cursor-grab">
        DURATION
    </div>
    <div class="myitem hover:bg-gray-300 hover:cursor-grab">
        PRICE
    </div>
    <div class="myitem hover:bg-gray-300 hover:cursor-grab">
        BUY
    </div>
    
    
  </div>

  <div v-for="(flightOffer, x) in flightData" :key="x">
    <div v-for="(fresh, y) in getFresh(flightOffer)" :key="y">
      <Row :item="fresh" />
      <br /><br />
    </div>
  </div> 
</template>

<style>
@tailwind base;
@tailwind components;
@tailwind utilities;

.mycont{
    display: flex;
    justify-content: space-around;
}
</style>
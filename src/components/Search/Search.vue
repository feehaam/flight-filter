<script>
import JsonFileData from "../../assets/data.json";
import Results from "../Display/Results.vue";

export default {
  name: "Search",
  data() {
    return {
      flightData: JsonFileData.flightOffer,
      tripType: "oneway",
      extraButtons: true,
      multiCity: true,
      from: "",
      to: "",
      startDate: "",
      returnDate: "",
      startTime: "",
      returnTime: "",
    };
  },
  methods: {
    searchData() {
      let from = document.getElementById("from").value;
      let to = document.getElementById("to").value;
      let startDate = document.getElementById("start_date").value;
      let returnDate = document.getElementById("return_date").value;
      let startTime = document.getElementById("start_time").value;
      let returnTime = document.getElementById("return_time").value;

      if (returnDate == null || returnDate.length < 4) {
        this.returnDate = null;
      } else this.returnDate = returnDate;
      if (startTime == null || startTime === "----") {
        this.startTime = null;
      } else this.startTime = startTime;
      if (returnTime == null || returnTime === "----") {
        this.returnTime = null;
      } else this.returnTime = returnTime;
      if (from !== null || from.length > 0) {
        this.from = from;
      } else {
        return;
      }
      if (to !== null || to.length > 0) {
        this.to = to;
      } else {
        return;
      }
      if (startDate) {
        this.startDate = startDate;
      } else {
        return;
      }
    },
    changeType(type) {
      this.tripType = type;
      if (type === "round") this.extraButtons = false;
      else this.extraButtons = true;
      if (type === "multi") this.multiCity = false;
      else this.multiCity = true;
    },
  },
  components: {
    Results,
  },
};
</script>

<template>
  <p class="text-gray-500 text-lg">Vue and Tailwind CSS in action</p>
  <button @click="changeType('oneway')">One way</button>
  <button @click="changeType('round')">Round trip</button>
  <button @click="changeType('multi')">Multi city</button>
  <br /><br />
  From: <input type="text" id="from" /> <br /><br />
  To: <input type="text" id="to" /> <br /><br />
  Date start: <input type="date" id="start_date" /> <br /><br />
  Date back: <input type="date" id="return_date" :disabled="extraButtons" />
  <br /><br />
  Time start:
  <select id="start_time">
    <option value="----">Select a time</option>
    <option value="00:00">00:00</option>
    <option value="01:00">01:00</option>
    <option value="02:00">02:00</option>
    <option value="03:00">03:00</option>
    <option value="04:00">04:00</option>
    <option value="05:00">05:00</option>
    <option value="06:00">06:00</option>
    <option value="07:00">07:00</option>
    <option value="08:00">08:00</option>
    <option value="09:00">09:00</option>
    <option value="10:00">10:00</option>
    <option value="11:00">11:00</option>
    <option value="12:00">12:00</option>
    <option value="13:00">13:00</option>
    <option value="14:00">14:00</option>
    <option value="15:00">15:00</option>
    <option value="16:00">16:00</option>
    <option value="17:00">17:00</option>
    <option value="18:00">18:00</option>
    <option value="19:00">19:00</option>
    <option value="20:00">20:00</option>
    <option value="21:00">21:00</option>
    <option value="22:00">22:00</option>
    <option value="23:00">23:00</option></select
  ><br /><br />
  Time back:
  <select id="return_time" :disabled="extraButtons">
    <option value="----">Select a time</option>
    <option value="00:00">00:00</option>
    <option value="01:00">01:00</option>
    <option value="02:00">02:00</option>
    <option value="03:00">03:00</option>
    <option value="04:00">04:00</option>
    <option value="05:00">05:00</option>
    <option value="06:00">06:00</option>
    <option value="07:00">07:00</option>
    <option value="08:00">08:00</option>
    <option value="09:00">09:00</option>
    <option value="10:00">10:00</option>
    <option value="11:00">11:00</option>
    <option value="12:00">12:00</option>
    <option value="13:00">13:00</option>
    <option value="14:00">14:00</option>
    <option value="15:00">15:00</option>
    <option value="16:00">16:00</option>
    <option value="17:00">17:00</option>
    <option value="18:00">18:00</option>
    <option value="19:00">19:00</option>
    <option value="20:00">20:00</option>
    <option value="21:00">21:00</option>
    <option value="22:00">22:00</option>
    <option value="23:00">23:00</option>
  </select>
  <br /><br />
  <button :disabled="multiCity">Add more</button><br /><br />
  <button @click="searchData()">Search</button><br /><br />
  <Results
    :flightData="flightData"
    :tripType="tripType"
    :inputFrom="from"
    :inputTo="to"
    :inputReturnDate="returnDate"
    :inputReturnTime="returnTime"
    :inputStartDate="startDate"
    :inputStartTime="startTime"
  />
</template>


<style>
@tailwind base;
@tailwind components;
@tailwind utilities;
</style>

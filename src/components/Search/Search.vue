<script>
import JsonFileData from "../../assets/data.json";
import Results from "../Display/Results.vue";

export default {
  name: "Search",
  //All necessary data
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
      // Collecting input from form
      let from = document.getElementById("from").value;
      let to = document.getElementById("to").value;
      let startDate = document.getElementById("start_date").value;
      let returnDate = document.getElementById("return_date").value;
      let startTime = document.getElementById("start_time").value;
      let returnTime = document.getElementById("return_time").value;

      // Responses, in case of invalid inputs
      if(from == null || from.length == 0) {
        alert("Type deperture location.");
        return;
      }
      if(to == null || to.length == 0) {
        alert("Type Arrival location.");
        return;
      }
      if(startDate == null || startDate.length < 6) {
        alert("Select a deperture date. ");
        return;
      }
      
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
    
    // Changing the trip type
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
  <div class="container md mx-auto px-4 border border-slate-300 rounded-xl shadow-md m-20 p-10 pl-10 pr-10">
    <div class="flex justify-center">
      <button @click="changeType('oneway')" class="bg-blue-500 hover:bg-blue-400 text-white font-bold mx-2 -mt-16 p-3 py-1 border-b-4 border-blue-700 hover:border-blue-500 rounded-xl">One way</button>
      <button @click="changeType('round')" class="bg-blue-500 hover:bg-blue-400 text-white font-bold mx-2 -mt-16 p-3 py-1 border-b-4 border-blue-700 hover:border-blue-500 rounded-xl">Round trip</button>
      <button @click="changeType('multi')" class="bg-blue-500 hover:bg-blue-400 text-white font-bold mx-2 -mt-16 p-3 py-1 border-b-4 border-blue-700 hover:border-blue-500 rounded-xl">Multi city</button>
    </div>
    <div class="flex justify-center mt-5">
      <input type="text" id="from" placeholder="From" class="border border-slate-300 m-2 py-2 px-5 rounded-xl shadow-md font-mono text-lg" />
      <input type="text" id="to" placeholder="To" class="border border-slate-300 m-2 py-2 px-5 rounded-xl shadow-md font-mono text-lg" />
    </div>
    <div class="flex justify-center">
      <div>
        <label for="start_date" class="font-serif text-sm m-3">Departure date</label><br>
        <input type="date" id="start_date" class="border border-slate-300 m-2 py-2 px-5 rounded-xl shadow-md font-mono text-lg"  /> 
      </div>
    <div>
      <label for="return_date" class="font-serif text-sm m-3">Return date</label><br>
      <input type="date" id="return_date" class="border border-slate-300 m-2 py-2 px-5 rounded-xl shadow-md font-mono text-lg"  :disabled="extraButtons" />
    </div>
    <div>
      <label for="start_time" class="font-serif text-sm m-3">Start time</label><br>
      <select id="start_time" class="border border-slate-300 m-2 py-2 px-5 rounded-xl shadow-md font-mono text-lg">
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
    </div>
    <div>
      <label for="return_time" class="font-serif text-sm m-3">Return date</label><br>
      <select id="return_time" class="border border-slate-300 m-2 py-2 px-5 rounded-xl shadow-md font-mono text-lg" :disabled="extraButtons">
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
    </div>
    <div>
      <label for="pas_type" class="font-serif text-sm m-3">Pas. type</label><br>
      <select id="pas_type" class="border border-slate-300 m-2 py-2 px-5 rounded-xl shadow-md font-mono text-lg">
        <option value="Adult">Adult</option>
        <option value="Child">Child</option>
        <option value="Infant">Infant</option>
      </select>
    </div>
    <div>
      <label for="tkt" class="font-serif text-sm m-3">Tickets</label><br>
      <input id="tkt" type="number" value="1" class="w-20 border border-slate-300 m-2 py-2 px-5 rounded-xl shadow-md font-mono" />
    </div>
  </div>
  <div class="flex justify-center">
    <button :hidden="multiCity" class="bg-gray-500 hover:bg-gray-400 text-white font-bold mx-2 p-3 py-1 border-b-4 border-gray-700 hover:border-gray-500 rounded-xl">Add more</button>
  </div>
  <div class="flex justify-center m-5">
    <button @click="searchData()" class="bg-red-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded-full shadow-xl border border-black-700">Search</button>
  </div>
  
  <div class="m-10">
    <hr>
  </div>


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

  </div>
</template>


<style>
@tailwind base;
@tailwind components;
@tailwind utilities;
</style>

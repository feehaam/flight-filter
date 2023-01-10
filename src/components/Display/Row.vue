<script>
export default {
  name: "Row",
  props: ["item", "tickets"],
  methods: {
    select(){
        alert("SELECTED FLIGHT \n--------------------\n"
        +"From: "+this.item.departurePlace+"\n"
        +"To: "+this.item.arrivalPlace+"\n"
        +"Class: "+this.item.class+"\n"
        +"Takeoff: "+this.item.departureTime+"\n"
        +"Arrival: "+this.item.arrivalTime+"\n"
        +"Duration: "+this.item.duration+"\n"
        +"Price per seat: "+this.item.price+"\n"
        )
    }
  }
};
</script>

<template>
    <div class="mycont border rounded-md shadow-sm p-2">
    <div class="myitem hover:bg-gray-300 hover:cursor-grab">
        {{ item.marketingCarrier }} {{ item.aircraft }}
    </div>
    <div class="myitem hover:bg-gray-300 hover:cursor-grab">
        {{ item.aircraft }} 
    </div>
    <div class="myitem hover:bg-gray-300 hover:cursor-grab">
        Class-{{ item.class }}
    </div>
    <div class="myitem hover:bg-gray-300 hover:cursor-grab">
        {{ item.fareBasis }}
    </div>
    <div class="myitem hover:bg-gray-300 hover:cursor-grab">
        {{ item.departurePlace }} - {{ item.arrivalPlace }}
    </div>
    <div class="myitem hover:bg-gray-300 hover:cursor-grab">
        {{ item.departureTime }}
    </div>
    <div class="myitem hover:bg-gray-300 hover:cursor-grab">
        {{ item.arrivalTime }}
    </div>
    <div class="myitem hover:bg-gray-300 hover:cursor-grab">
        {{ item.duration }}
    </div>
    <div class="myitem hover:bg-gray-300 hover:cursor-grab">
        {{ item.price }}
    </div>
    <button class="myitem bg-green-500 hover:bg-green-700 text-white font-bold py-1 px-4 rounded-md shadow-xl border border-black-700" @click="select()">SELECT</button>
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
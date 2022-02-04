<template>
    <div class="slide">
        <div class="slide-headline">{{headline}}</div>
        <select class="input dropdown-select" v-model="selectedVehicle" autofocus @change="onSelect">
            <option class="null-option" disabled selected hidden value="default" key="-1"> --select one-- </option>
            <option class="dropdown-option" v-for="(vehicle, idx) in vehicles" :value="vehicle" :key="idx">{{vehicle}}</option>
        </select>
    </div>
</template>

<script>
import {VEHICLES} from "../../data.js"

export default {
    name: "VehicleSlide",
    data() {
        return {
            headline: "What kind of vehicle would you like to reserve?",
            vehicles: VEHICLES,
            selectedVehicle: "default"
        }
    },
    methods: {
        onSelect(e) {
            const vehicle = e.target.value
            this.$emit("selected-vehicle", vehicle)
        }
    },
}
</script>

<style>
.input {
    font-size: 20px;
    text-align: center;
    width: 150px;
    padding: 2px;
    margin: 10px;
    font-family: 'Open Sans', sans-serif;
}
.input.dropdown-select {
    width: 157px;
}


</style>
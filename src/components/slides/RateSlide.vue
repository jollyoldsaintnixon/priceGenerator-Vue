<template>
    <div class="slide">
        <div class="slide-headline">{{headline}}</div>
        <select class="input dropdown-select" v-model="selectedRate" autofocus @change="onSelect">
            <option class="null-option" disabled selected hidden value="default" key="-1"> --select one-- </option>
            <option class="dropdown-option" v-for="(rate, idx) in rates" :value="rate" :key="idx">{{rate}}</option>
        </select>
    </div>
</template>

<script>
import {makePlural, convertToWord} from "../../helpers"
import {RATES} from "../../data"

export default {
    name: "RateSlide",
    props: {
        selectedVehicle: String,
        selectedAmount: Number,
    },
    data() {
        return {
            rates: RATES,
            selectedRate: "default"
        }
    },
    methods: {
        onSelect(e) {
            const rate = e.target.value
            this.$emit("selected-rate", rate)
        }
    },
    computed: {
        headline() {
            return ("Alright, " 
            + convertToWord(this.selectedAmount) + " " + makePlural(this.selectedVehicle, this.selectedAmount) +
            ". How would you like to measure your reservation- by days, hours or distance driven?")
        }
    },
}
</script>

<style>

</style>
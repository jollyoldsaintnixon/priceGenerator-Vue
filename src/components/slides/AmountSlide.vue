<template>
    <div class="slide">
        <div class="slide-headline">{{headline}}</div>
        <input class="input" type="number" min="0" autofocus v-model="selectedAmount" @change="onSelect" /> 
    </div>
</template>

<script>
import {makePlural} from "../../helpers.js" 

export default {
    name: "AmountSlide",
    props: {
        selectedVehicle: {
            type: String,
            required: false
        }
    },
    data() {
        return {
            selectedAmount: 0,
        }
    },
    methods: {
        onSelect(e) {
            console.log(e)
            const amount = e.target.value
            this.$emit("selected-amount", amount)
        }
    },
    computed: {
        headline() {
            if (this.selectedVehicle) {
                return "How many " + makePlural(this.selectedVehicle) + " would you like to reserve?"
            } else {
                return "Please select a vehicle"
            }
        }
    },
}
</script>

<style>

</style>
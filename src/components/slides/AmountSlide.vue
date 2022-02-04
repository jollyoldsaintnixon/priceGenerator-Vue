<template>
    <div class="slide">
        <div class="slide-headline">{{headline}}</div>
        <input class="input" type="number" min="0" autoFocus v-model="selectedAmount" @change="onSelect" /> 
    </div>
</template>

<script>
import {makePlural} from "../../helpers.js" 
// <p className="slide-headline">How many {makePlural(this.props.selectedVehicle)} would you like to reserve?</p>
// <input className="input" type="number" min="0" autoFocus value={selectedAmount} onChange={e => this.props.onSelect(e)}></input>

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
            selectedAmount: null,
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
    components: {

    },
}
</script>

<style>

</style>
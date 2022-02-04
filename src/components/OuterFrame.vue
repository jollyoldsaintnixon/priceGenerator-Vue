<template>
    <div class="outer-frame">
        <div class="leed">{{ headline }}</div>
        <div class="card" >
            <VehicleSlide v-show="slideNum === 0" @selected-vehicle="updateSelectedVehicle" />
            <AmountSlide v-show="slideNum === 1" @selected-amount="updateSelectedAmount" 
                :selectedVehicle="selectedVehicle"/>
            <RateSlide v-show="slideNum === 2" @selected-rate="updateSelectedRate" 
                :selectedVehicle="selectedVehicle" :selectedAmount="selectedAmount"/>
            <UnitsSlide v-show="slideNum === 3" @selected-units="updateSelectedUnits" 
             :selectedVehicle="selectedVehicle" :selectedAmount="selectedAmount" :selectedRate="selectedRate"/>
            <SubmitSlide v-show="submitted" @selected-units="updateSelectedUnits" :submitted="submitted"
            :selectedVehicle="selectedVehicle" :selectedAmount="selectedAmount" :selectedRate="selectedRate" :selectedUnits="selectedUnits" />
            <Navigator 
                :slideNum="slideNum"
                :selectedVehicle="selectedVehicle"
                :selectedAmount="selectedAmount"
                :selectedRate="selectedRate"
                :selectedUnits="selectedUnits"
                :ready="readyToSubmit"
                @prev-slide="onPrevSlide"
                @next-slide="onNextSlide"
                @submitted="onSubmit"
            />
        </div>
    </div>
</template>

<script>
import Navigator from "./Navigator.vue"
import VehicleSlide from './slides/VehicleSlide.vue'
import AmountSlide from './slides/AmountSlide.vue'
import RateSlide from './slides/RateSlide.vue'
import UnitsSlide from './slides/UnitsSlide.vue'
import SubmitSlide from './slides/SubmitSlide.vue'

export default {
    name: "OuterFrame",
    props: {},
    data() {
        return {
            headline: "Get a free quote!",
            slideNum: 0,
            selectedVehicle: null,
            selectedAmount: null,
            selectedRate: null,
            selectedUnits: null,
            submitted: false,
        }
    },
    methods: {
        updateSelectedVehicle(vehicle) {
            this.selectedVehicle = vehicle
        },
        updateSelectedAmount(amount) {
            this.selectedAmount = amount
            console.log(this.selectedAmount)
        },
        updateSelectedRate(rate) {
            this.selectedRate = rate
        },
        updateSelectedUnits(units) {
            this.selectedUnits = units
        },
        onPrevSlide() {
            this.slideNum -= 1
            this.submitted = false // reset that
        },
        onNextSlide() {
            this.slideNum += 1
        },
        onSubmit() {
            this.submitted = true,
            this.slideNum = 4 // one more than amount of slides
        }
    },
    computed: {
        readyToSubmit() {
            return (this.selectedAmount && 
            this.selectedRate && this.selectedAmount > 0 && 
            this.selectedUnits && this.selectedUnits > 0 &&
            this.selectedVehicle)
        }
    },
    components: {
        Navigator,
        VehicleSlide,
        AmountSlide,
        RateSlide,
        UnitsSlide,
        SubmitSlide,
    },
}
</script>

<style>
.leed {
    font-size: 40px;
    margin: 20px;
}
.outer-frame {
    margin: auto;
    margin-top: 50px;
    width: 50%;
    display: flex;
    flex-direction: column;
    justify-content: center;
}
.card {
    box-shadow: -5px 2px 10px #bae5fb;
    border-radius: 25px;
}
.slide {
    display: flex;
    flex-direction: column;
    justify-content: space-around;
    align-items: center;
    background-color: #fff;
    border-radius: 4px;
    max-width: 400px;
    margin: 10% auto;
    height: 100px;
    position: relative;
    padding: 34px;
}
.slide-headline {
    margin: auto;
    margin-bottom: 30px;
}
.null-option {
    font-style: italic;
    color: gray;
}

</style>
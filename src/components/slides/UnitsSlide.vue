<template>
    <div class="slide">
        <p className="slide-headline">{{headline}}</p>
        <input class="input" type="number" min="0"  autoFocus v-model="selectedUnits" @change="onSelect"/>
    </div>
</template>

<script>
import { DAILY, HOURLY, DISTANCE } from "../../data"
import { makePlural } from '../../helpers';

export default {
    name: "UnitsSlide",
    props: {
        selectedRate: String,
    },
    data() {
        return {
            selectedUnits: null,
        }
    },
    methods: {
        onSelect(e) {
            const units = e.target.value
            this.$emit("selected-units", units)
        }
    },
    computed: {
        headline() {
            let sentenceEnd = ""
            let pluralized = makePlural(this.selectedVehicle, this.selectedAmount)
            switch (this.selectedRate) {
                case DAILY:
                    sentenceEnd = "for how many days will you need the " + pluralized + "?"
                    break
                case HOURLY:
                    sentenceEnd = "for how many hours will you need the " + pluralized  + "?"
                    break
                case DISTANCE:
                    sentenceEnd = "how many miles do you expect to cover?"
        }
            return (
                "And finally, " + sentenceEnd
            )
        }
    },
}
</script>

<style>

</style>
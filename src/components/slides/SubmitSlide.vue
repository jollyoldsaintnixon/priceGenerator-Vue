<template>
    <div class="slide slide-submit">
        <p className="submit-headline">${{generatedPrice}}</p>
        <p className="submit-details">{{details}}</p>
    </div>
</template>

<script>
import { PRICE_SHEET, DAILY, HOURLY, DISTANCE } from "../../data";
import { makePlural, convertToWord } from "../../helpers";
console.log("hey")
export default {
    name: "SubmitSlide",
    props: {
        selectedRate: String,
        selectedUnits: Number,
        selectedVehicle: String,
        selectedAmount: Number,
        submitted: Boolean
    },
    computed: {
        details() {
            const converted = convertToWord(this.selectedUnits)
            const amountInWords = convertToWord(this.selectedAmount)
            const pluralized = makePlural(this.selectedVehicle, this.selectedAmount)
            switch (this.selectedRate) {
                case DAILY:
                    return amountInWords + " " + pluralized + " for " + converted + " days."
                case HOURLY:
                    return amountInWords + " " + pluralized + " for " + converted + " hours."
                case DISTANCE:
                    return amountInWords + " " + pluralized + " for " + converted + " miles."
            }
            return "total"
        },
        generatedPrice() {
            if (this.submitted) return PRICE_SHEET[this.selectedVehicle][this.selectedRate] * this.selectedUnits * this.selectedAmount
            return "Please fill out the rest of the form"
        }
    },
}
</script>

<style>
.submit-headline {
    font-size: xxx-large;
    color: #08a6f0;
    margin-bottom: 30px;
}
</style>
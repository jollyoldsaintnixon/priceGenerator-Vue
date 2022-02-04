<template>
    <div class="navigator">
        <div class="button prev" :class="{unlocked: unlockedBack}" @click="onPrev">
            <i class="material-icons" style="{color: unlockedBackColor}">
                arrow_left</i>
        </div>
        <div class="button submit-button" :class="{unlocked: ready}" @click="onSubmit">Submit</div>
        <div class="button next" :class="{unlocked: unlockedNext}" @click="onNext">
            <i className="material-icons" style="{color: unlockedNextColor}">
                    arrow_right</i>
        </div>
    </div>
</template>



<script>
        // const unlockedBack = this.unlockBack() // lots of variables; probably could have made it more of a function
        // const unlockedBackColor = unlockedBack ? "#08a6f0" : "gray"
        // const unlockedBackClass = unlockedBack ? " unlocked" : ""
        // const unlockedNext = this.unlockNext()
        // const unlockedNextColor = unlockedNext ? "#08a6f0" : "gray"
        // const unlockedNextClass = unlockedNext ? " unlocked" : ""
        // const ready = this.checkReady()
        // const readyClass = ready ? " unlocked" : ""
        // return (
        //     <div className="navigator">
            
        //         <a className={"button prev" + unlockedBackClass} onClick={(e) => {
        //                 if (unlockedBack) {
        //                 return this.props.onBack(e)
        //                 } return
        //             }}><i class="material-icons" style={{color: unlockedBackColor}}>
        //         arrow_left</i></a>
        //         <a className={"button submit" + readyClass} onClick={(e) => {
        //                 if (ready) {
        //                     return this.props.onSubmit(e)
        //                 } return
        //             }}>Submit</a>
        //         <a className={"button next" + unlockedNextClass} 
        //         onClick={(e) => {
        //                 if (unlockedNext) {
        //                     return this.props.onNext(e)
        //                 } return
        //             }}><i className={"material-icons"} style={{color: unlockedNextColor}}>
        //             arrow_right</i></a>
        //     </div>
        // )

export default {
    name: "Navigator",
    props: {
        slideNum: {
            type: Number,
            required: true,
        },
        selectedVehicle: {
            type: String,
            required: false,
            default: null
        },
        selectedAmount: {
            type: Number,
            required: false,
            default: null
        },
        selectedRate: {
            type: String,
            required: false,
            default: null
        },
        selectedUnits: {
            type: Number,
            required: false,
            default: null
        },
        ready: {
            type: Boolean,
            required: true
        }
    },
    data() {
        return {
            
        }
    },
    methods: {
        onNext() {
            switch (this.slideNum) {
                case 0:
                    if (this.selectedVehicle) this.$emit("next-slide")
                    break
                case 1:
                    if (this.selectedAmount && this.selectedAmount > 0) this.$emit("next-slide")
                    break
                case 2:
                    if (this.selectedRate) this.$emit("next-slide")
                    break
                case 3: // no next for units
                    break
            }
        },
        onPrev() {
            switch (this.slideNum) {
                case 0: // no prev for vehicle
                    break
                default: // otherwise can always go back
                    this.$emit("prev-slide")
            }
        },
        onSubmit() {
            if (this.ready) {
                this.$emit("submitted")
            }
        }
    },
    computed: {
        unlockedBack() {
            return (this.slideNum > 0)
        },
        unlockedBackColor() {
            return this.unlockedBack ? "#08a6f0" : "gray"
        },
        unlockedNext() {
            switch (this.slideNum) {
                case 0:
                    if (this.selectedVehicle) return true
                    break
                case 1:
                    if (this.selectedAmount && this.selectedAmount > 0) return true
                    break
                case 2:
                    if (this.selectedRate) return true
                    break
                case 3: // no next for units
                    break
                    }
            return false
        },
        unlockedNextColor() {
            return this.unlockedNext ? "#08a6f0" : "gray"
        },
    }
}
</script>

<style scoped>
.navigator {
    margin: 10px;
    display: flex;
    justify-content: center;
}
.button {
    margin: 10px;
}
.submit-button {
    padding: 14px 0;
    color: #fff;
    font-size: 20px;
    letter-spacing: .64px;
    border-radius: 25.5px;
    background-color: gray;
    width: 148px;
}

.material-icons {
    font-size: 50px;
}

.unlocked {
    color: #08a6f0;
    /* box-shadow: 0 9px 16px 0 #bae5fb; */
}

.unlocked:hover {
    cursor: pointer;
}

.submit-button.unlocked {
    background-color: #08a6f0;
    color: white;
    /* box-shadow: 0 9px 16px 0 #bae5fb; */
}

</style>

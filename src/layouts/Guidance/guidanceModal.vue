<template>
    <div>
        <iv-modal :positionModal="guidanceInput.positionModal" >
            <template #header style="positon:relative" >
                <iv-button v-if="homeButton" @click="goHome" class="home-button" >Home</iv-button>
                <div>{{guidanceHeaderText}}</div>
                <iv-button @click="closeWindow" class="close-button" >X</iv-button>
            </template>
            <template>
                <div>{{guidanceInput.text}}</div>
            </template>
            <template #footer>
                <iv-button v-if="prevButton" @click="prevGuidance">PREV</iv-button>
                <iv-button v-if="nextButton" @click="nextGuidance">NEXT</iv-button>
            </template>
        </iv-modal>
    </div>
</template>

<script>
import Button from "../../components/Button";
import windowModal from "../WindowComp";
import guidanceBus from "buses/guidanceBus"
export default {
    name:"iv-guidance-modal",
    components:{
        "iv-modal":windowModal,
        "iv-button":Button
    },
    props:{
        guidanceHeaderText:{
            type: String,
            default: "Help!"
        },
        guidanceInput:{
            type:Object
        },
        prevButton:{
            type:Boolean,
            default:false
        },
        nextButton:{
            type:Boolean,
            default:false
        },
        homeButton:{
            type:Boolean,
            default:false
        },
    },
    methods:{
        guidanceAction(event){
            document.getElementById(this.guidanceInput.highlightDiv).style.zIndex = 0;
            document.getElementById(this.guidanceInput.highlightDiv).style.pointerEvents = "auto";
            guidanceBus.$emit("hide-component", this.guidanceInput.highlightDiv);
            guidanceBus.$emit(event, this._uid);
        },
        prevGuidance(){
            this.guidanceAction('prev-guidance')
        },
        nextGuidance(){
            this.guidanceAction('next-guidance')
        },
        closeWindow(){
            this.guidanceAction('close-window')
        },
        goHome(){
            this.guidanceAction('go-home')
        }
    },
    mounted(){
        guidanceBus.$emit("show-component", this.guidanceInput.highlightDiv);
        document.getElementById(this.guidanceInput.highlightDiv).style.zIndex = 220;
        document.getElementById(this.guidanceInput.highlightDiv).style.pointerEvents = "none";
    },
    watch:{
        guidanceInput:function(){
            guidanceBus.$emit("show-component", this.guidanceInput.highlightDiv);
            document.getElementById(this.guidanceInput.highlightDiv).style.zIndex = 220;
            document.getElementById(this.guidanceInput.highlightDiv).style.pointerEvents = "none";
        }
    }
}
</script>
<style>
</style>
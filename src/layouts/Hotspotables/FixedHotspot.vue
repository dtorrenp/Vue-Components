<template>
    <div class="iv-hotspotable iv-fixed-hotspot" :style="setSize">
        <slot/>
    </div>
</template>
<script>
import Hotspotable from 'mixins/Hotspotable.js'
export default {
    name:"iv-fixed-hotspot",
    mixins:[Hotspotable],
    props:{
        size:{
            type:Number,
            required:false,
            default:300
        },
        direction:{
            type:String,
            required:false,
            default:"auto"
        },

    },
    computed:{
        setSize(){
            
            return { }
        }
    }
}
</script>
<style lang="scss">
.iv-fixed-hotspot{
    display:flex;
    flex: 1 1 auto; // Grow box to size
    &.iv-left{
        
    }
    &.iv-right{

    }
    &.iv-top{

    }
    &.iv-bottom{

    }
    &.iv-bottomleft{
        width:100%;
        height:100%;
    }
    &.iv-bottomright{
        width:100%;
        height:100;
    }
    &.iv-topright{
        width:100%;
        height:100%;
    }
    &.iv-topleft{
        width:100%;
        height:100%;
    }
}

</style>
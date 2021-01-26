<template>
    <div class="select" @click="openOptions">

        <div class="selected" :class="{focus: !isClose}">
            <div class="label">
                <FontAwesomeIcon  v-if="iconSelected" class="before-icon" :icon="iconSelected" :key="iconSelected"/>
                <span>{{hint}}</span>
            </div>
            <div class="icon" :class="{focus_background: !isClose}">
                <FontAwesomeIcon :icon="iconDown" :key="iconDown"/>
            </div>
            
        </div>
        <Items 
            :placeHolder="hint" 
            :onPlaceHolder="handlePlaceHolder" 
            :isClose="isClose" 
            v-bind:items="items" 
            :multiselect="multiSelect"
            :onIconSelected="handleIcon"/>
    </div>
</template>

<script>
import { library } from '@fortawesome/fontawesome-svg-core'
import { faChevronDown, faChevronUp } from '@fortawesome/free-solid-svg-icons'
import { FontAwesomeIcon } from '@fortawesome/vue-fontawesome'
library.add(faChevronDown, faChevronUp)
import Items from './Items';
const props = {
    items: [Array],
    multiselect: {
        type:Boolean,
        default: false
    },
    placeholder: String

}
export default {
    name:'Select',
    props,
    components: {
        FontAwesomeIcon,
        Items
    },
    data() {
        return {
            isClose: true,
            hint: this.placeholder,
            iconSelected: '',
            multiSelect:this.multiselect,
            iconDown: 'chevron-down'
        }
    },
    methods: {
        handlePlaceHolder(value) {
            this.hint = value;

        },
        handleIcon(value) {
            this.iconSelected = value;
            console.log(this.iconSelected)
        },
        openOptions() {
            this.isClose = !this.isClose
            if (this.isClose) this.iconDown = 'chevron-down'
            else this.iconDown = 'chevron-up'
        }
    }
}
</script>

<style scoped>
.select {
    width: 350px;
    cursor: pointer;
}
.selected {
    width: 100%;
    height: 56px;
    display: flex;
    border: 1px solid #dbe3e2;
    border-radius: 5px;
}
.icon {
    background-color: #f6f8f7;
}
.icon {
    width: 20%;
    display: flex;
    justify-content: center;
    align-items: center;
    margin-left: 20px;
    border-radius: 0px 5px 5px 0px;
    background: transparent;
}
.selected .icon {
    border-left: 1px solid #dbe3e2;
}
.label {
    width: 80%;
    display: flex;
    align-items: center;
    margin-left: 20px;
}
.items-container {
    width: 350px;
    position: absolute;
    z-index: 2;
    border-left: 1px solid #dbe3e2;
    border-bottom: 1px solid #dbe3e2;
    border-right: 1px solid #dbe3e2;
    border-radius: 0px 0px 5px 5px;
    box-shadow: 0px 2px 3px 0px gray;
}
.is_close {
    display:none
}
.item {
    height: 56px;
    display: flex;
    align-items: center;
    cursor: pointer;

}
.item:hover {
     background-color: #e3f6ef;
}
.before-icon {
    margin-right: 8px;
}
.focus {
    border: 1px solid #55b685;
    border-radius: 5px 5px 0px 0px !important;
    box-shadow: 0px 1px 3px 0px gray;
}
.focus_background {
    background-color: #e3f6ef;
    border-left: 1px solid #55b685 !important;
    border-radius: 0px 5px 0px 0px !important;
}
.background_checked {
    background-color: #f6f8f7;
    
}
.background_checked .icon {
    color: #55b685;
}

</style>
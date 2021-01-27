<template>
    <div class="select"  @click="openOptions">

        <div class="selected" :class="{focus: !isClose, selected_small: isSmall}">
            <div class="label" :class="{margin_label: !iconSelected}">
                <FontAwesomeIcon  v-if="iconSelected" class="before-icon" :icon="iconSelected" :key="iconSelected"/>
                <span>{{hint}}</span>
            </div>
            <div class="icon" :class="{focus_background: !isClose, icon_small: isSmall}">
                <FontAwesomeIcon :icon="iconDown" :key="iconDown" class="icon_down" :class="{icon_up: iconDown !== 'chevron-down', icon_down_small: isSmall}"/>
            </div>
            
        </div>
        <Items 
            :placeHolder="hint" 
            :onPlaceHolder="handlePlaceHolder" 
            :isClose="isClose" 
            v-bind:items="items" 
            :multiselect="multiSelect"
            :onIconSelected="handleIcon"
            :isSmall="isSmall"/>
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
    placeholder: String,
    isSmall: {
        type:Boolean,
        default: true
    }

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
.selected_small {
    height: 44px;
}
.icon {
    background-color: #f6f8f7;
}
.icon {
    width: 48px;
    display: flex;
    justify-content: center;
    align-items: center;
    border-radius: 0px 5px 5px 0px;
    background: transparent;
}
.icon_small {
    width: 44px;
}
.selected .icon {
    border-left: 1px solid #dbe3e2;
}
.icon_up {
    color: #55b685;
}
.icon_down {
    width: 16px;
    height: 16px;
    margin: 10px;
}
.icon_down {
    width: 16px;
    height: 16px;
    margin: 8px;
}
.label {
    width: 100%;
    display: flex;
    align-items: center;
}
.margin_label {
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
    width: 16px;
    height: 16px;
    margin-right: 16px;
    margin-top: 16px;
    margin-bottom: 16px;
    margin-left: 12px;
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
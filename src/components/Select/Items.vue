<template>
    <div class="items-container" :class="{is_close: this.isClose}">
        <div class="item"
            :class="{background_checked:item.checked, item_small: isSmall}"
            @click="clickItem(item)"
            v-for="item in dataItems"
            :key="item.name">
            <div class="label" :class="{margin_label: !item.icon}">
                <FontAwesomeIcon v-if="item.icon" class="before-icon" :icon="item.icon"/>
                <span>{{item.name}}</span>
            </div>
            <div class="icon" v-if="item.checked">
                <FontAwesomeIcon :icon="['fas', 'check']" class="icon_check" :class="{icon_check_small: isSmall}"/>
            </div>
        </div>
    </div>
</template>

<script>
import { library } from '@fortawesome/fontawesome-svg-core'
import { faCheck } from '@fortawesome/free-solid-svg-icons'
import { FontAwesomeIcon } from '@fortawesome/vue-fontawesome'
library.add(faCheck)
export default {
    components: {
        FontAwesomeIcon
    },
    props: [
        'multiselect',
        'items',
        'onPlaceHolder',
        'isClose',
        'placeHolder',
        'iconSelected',
        'onIconSelected',
        'isSmall'
    ],
    data() {
        return {
            dataItems: this.items,
            placeHolderTemp: this.placeHolder,
            placeH: this.placeHolder,
            labelSelected: []
        }
    },
    methods: {
        setPlaceHolder : function (value) {
            this.placeH = `${this.placeH} ${value}`;
            this.onPlaceHolder(this.placeH);
        },
        clickItem: function(item) {
            if (this.multiselect) {
                this.placeH = '';
                item.checked = !item.checked
                if (item.checked) this.labelSelected.push(item.name)
                else this.labelSelected = this.labelSelected.filter(label => label !== item.name)
                if (this.labelSelected.length === 0) this.onPlaceHolder(this.placeHolderTemp)
                this.labelSelected.forEach(label => this.setPlaceHolder(label));
            } else {
                this.items.forEach(element => {
                    element.checked = false
                });
                item.checked = true;
                this.onPlaceHolder(item.name);
                this.onIconSelected(item.icon);

            }

        }
    }
}
</script>
<style scope>
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
.item {
    height: 56px;
    display: flex;
    align-items: center;
    cursor: pointer;

}
.item_small {
    height: 40px;

}
.label {
    width: 100%;
    display: flex;
    align-items: center;
    height: 100%;
}
.item:hover {
     background-color: #e3f6ef;
}
.margin_label {
    margin-left: 20px;
}

.background_checked {
    background-color: #f6f8f7;
    
}
.icon {
    background-color: #f6f8f7;
}
.icon {
    display: flex;
    justify-content: center;
    align-items: center;
    border-radius: 0px 5px 5px 0px;
    background: transparent;
}
.before-icon {
    width: 16px;
    height: 16px;
    margin-right: 16px;
    margin-top: 16px;
    margin-bottom: 16px;
    margin-left: 12px;
}
.icon_check_small {
    margin: 8px;
}
.icon_check {
    width: 16px !important;
    height: 16px;
    margin: 10px;
    color: #55b685;
}

.is_close {
    display:none
}
</style>
<template>
    <div class="items-container" :class="{is_close: this.isClose}">
        <div class="item"
            :class="{background_checked:item.checked}"
            @click="clickItem(item)"
            v-for="item in dataItems"
            :key="item.name">
            <div class="label">
                <FontAwesomeIcon class="before-icon" :icon="item.icon"/>
                <span>{{item.name}}</span>
            </div>
            <div class="icon" v-if="item.checked">
                <FontAwesomeIcon :icon="['fas', 'check']"/>
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
    props: ['multiselect', 'items', 'onPlaceHolder', 'isClose', 'placeHolder', 'iconSelected', 'onIconSelected'],
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
.label {
    width: 80%;
    display: flex;
    align-items: center;
    margin-left: 20px;
}
.item:hover {
     background-color: #e3f6ef;
}

.background_checked {
    background-color: #f6f8f7;
    
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
.before-icon {
    margin-right: 8px;
}

.is_close {
    display:none
}
</style>
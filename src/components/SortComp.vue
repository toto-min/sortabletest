<template>
    <div style="display: flex; align-items: start; justify-content: center;">
        <div style="margin-right: 30px;">
            <ul>
            <li :key="item.id" :id="item.id" v-for="item in itemcont" style="width: 200px; height: 200px; border: 1px solid;" :style="{ 'background-color' :item.color}">
                {{ item.num + 1 }}
                <div :id="item.num">
                    <span>
                        {{ item.name }}
                    </span>
                </div>
                <div class="contbody">
                    {{ item.id }} {{ item.name }}
                </div>
            </li>
        </ul>
        </div>
        <div>
            <draggable 
                v-model="itemlist"
                @start="drag=true" 
                @end="drag=false"
                :component-data="getComponentData()"
                handle=".handle"
                item-key="id">
                <template #item="{element}">
                    <div style="display: flex; align-items: center; justify-content: space-between;">
                        <div class="handle"></div>
                        <div>{{element.name}}</div>
                    </div>
                </template>
            </draggable>
            <div>
                <button @click="addlist">add btn</button>
            </div>
        </div>
    </div>
</template >
<script>
// import Sortable from 'sortablejs'
// import _ from 'lodash'
  import draggable from 'vuedraggable'
  export default {
        components: {
            draggable,
        },
        data() {
          return {
            drag: false,
            itemlist: [
                {
                    id: 1,
                    name: 'list1',
                },
                {
                    id: 2,
                    name: 'list2',
                },
                {
                    id:3,
                    name: 'list3',
                }
            ],
            itemcont: [],
            contlist: [
                {
                    id: 1,
                    name: 'cont1',
                    num: 0,
                    color: 'red'
                },
                {
                    id:2,
                    name: 'cont2',
                    num: 1,
                    color: 'blue'
                },
                {
                    id:3,
                    name: 'cont3',
                    num: 2,
                    color: 'green'
                }
            ],
            activeNames:''
          }            
        },
        created() {
            this.contlist.forEach(el => {
                this.itemcont.push(el)
            })
        },
        methods: {
            addlist() {
                let el = {
                    id:4,
                    name: 'cont4',
                    num: 3,
                    color: 'yellow'
                }
                this.itemlist.push(el)
                this.contlist.push(el)
                this.itemcont.push(el)
            },
            handleChange(toval) {
                let tempitem = this.itemcont[toval.oldIndex]
                this.itemcont.splice(toval.oldIndex, 1)
                this.itemcont.splice(toval.newIndex, 0, tempitem)
            },
            inputChanged(value) {
                console.log(value);
            },
            getComponentData() {
            return {
                onEnd: this.handleChange,
                onInput: this.inputChanged,
                wrap: true,
                value: this.activeNames
            };
            }
        }
    }
</script>
<style>
*{
    margin: 0;
    padding: 0;
}
ul, li {
    list-style: none;
}
.list_item {
    height: 30px;
    border: 1px solid;
}

.my-handle {
	cursor: move;
	cursor: -webkit-grabbing;
}

.handle{
    width: 10px;
    height: 10px;
    border-radius: 50%;
    background-color: #000000;
}
</style>
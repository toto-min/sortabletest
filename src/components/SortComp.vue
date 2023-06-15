<template>
    <div>
        <draggable 
            v-model="itemlist"
            @start="drag=true" 
            @end="drag=false"
            :component-data="getComponentData()"
            item-key="id">
            <template #item="{element}">
                <div>{{element.name}}</div>
            </template>
        </draggable>

        <ul>
            <li :key="item.id" :id="item.id" v-for="item in itemcont" style="width: 300px; height: 300px; border: 1px solid; float: left;">
                {{ item.num + 1 }}
            </li>
        </ul>
    </div>
</template>
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
                    num: 0
                },
                {
                    id:2,
                    name: 'cont2',
                    num: 1
                },
                {
                    id:3,
                    name: 'cont3',
                    num: 2
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
</style>
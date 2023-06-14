<template>
    <div>
        <ul id="items" style="margin: 0 auto; width: 500px;">
            <li style="width: 500px; height: 500px; background-color: blue;"></li>
            <li style="width: 500px; height: 500px; background-color: red;"></li>
        </ul>
    </div>
</template>
<script>
import Sortable from 'sortablejs'
//   import draggable from 'vuedraggable'
  export default {
        components: {
            // draggable,
        },
        data() {
          return {
            drag: false,
            myArray: [
                {
                    id: 1,
                    name: 'list1'
                },
                {
                    id:2,
                    name: 'list2'
                },
                {
                    id:3,
                    name: 'list3'
                }
            ]
          }
        },
        mounted() {
            var el = document.getElementById('items');
            new Sortable(el, {
                swapThreshold: 0.78,
                animation: 150
            });
        },
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
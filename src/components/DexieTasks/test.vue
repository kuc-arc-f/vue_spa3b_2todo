<template>
    <div>
        <h1>DoxieTasks- test:</h1>
        <hr />
        data : {{ data1 }}

    </div>
</template>

<script>
import {Mixin} from '../../mixin'
import Dexie from 'dexie';

var db = new Dexie("friend_database");
//
export default {
    mixins:[Mixin],
    created() {
          db.version(1).stores({
              friends: 'name,shoeSize'
          });
          this.add_item()
          this.get_items()
    },
    data() {
        return {
            user : [],
            message : "data: Hello-TestChild-123",
            child_data : "hoge",
            data1 : "",
        }
    },
    methods: {
        getTasks(){
        },
        add_item(){
            // name: "Nicolas", shoeSize: 8p
            db.friends.add({
                name: "Nicolas", 
                shoeSize: 8,
            });
            db.friends.add({
                name: "Kotan", 
                shoeSize: 6,
            });

        },
        get_items(){
            db.friends
                .toArray()
                .then(function (items ) {
                    console.log( items );
                });
        },

    }
}
</script>


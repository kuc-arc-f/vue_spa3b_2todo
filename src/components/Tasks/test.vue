<template>
    <div>
        <h1>Tasks- test:</h1>
        <hr />
        <!--
        test : {{ message }}
            -->
        <TestChild :child_data=child_data :objects=objects ></TestChild>
    </div>
</template>

<script>
import axios from 'axios'
import {Mixin} from '../../mixin'
//import LibTest from '@/libs/LibTest';
import TestChild from '../../components/Element/TestChild'

//
export default {
    mixins:[Mixin],
    components: { TestChild },
    created() {
//        LibTest.func2()
//console.log( this.sysConst.URL_BASE )
    },
    data() {
        return {
            user : [],
            message : "data: Hello-TestChild-123",
            child_data : "hoge",
            objects: [
                {
                    id: 1,
                    number: 10,
                    name: '山田太郎'
                },
                {
                    id: 2,
                    number: 11,
                    name: '山田2'
                },
            ]
        }
    },
    methods: {
        getTasks(){
            var url = this.sysConst.URL_BASE +'/api/test_tasks'
console.log(url)
            axios.get(url).then(res =>  {
                this.tasks = res.data
//                console.log(res.data.length )
console.log( this.tasks )
            })            

        },
    }
}
</script>


<template>
    <div class="task_index_wrap">
        <FlashMessage></FlashMessage>
        <h3>IndexTasks</h3>
        <hr class="mt-2 mb-2" />
        <router-link :to="'/dexie_tasks/new/'" class="btn btn-primary">Create</router-link>
        <hr class="mt-2 mb-2" />
        <br />
        <ul v-for="task in tasks" v-bind:key="task.id">
            <li>
                <router-link :to="'/dexie_tasks/show/' + task.id">{{ task.title }}</router-link>
                &nbsp;&nbsp;
                <router-link :to="'/dexie_tasks/edit/' + task.id"
                 class="btn btn-outline-primary btn-sm">Edit
                </router-link>                
                <br />
                ID : {{ task.id }}
                , {{ task.created_at }}
            </li>
        </ul>
        <hr />
        <div class="page_info_wrap">
            <ul>
                <li>このページの機能は、オープンソースで公開しております。<br />
                    <a  href='https://github.com/kuc-arc-f/vue_spa3b_1crud'>
                        https://github.com/kuc-arc-f/vue_spa3b_1crud 
                    </a><br />
                    <br />
                </li>
                <li>関連ブログ:<br />
                    <a  href='https://knaka0209.hatenablog.com/entry/indexed_db_1'>
                        https://knaka0209.hatenablog.com/entry/indexed_db_1
                    </a><br />
                </li>
            </ul>
        </div>        
    </div>
</template>

<!-- -->
<style> 
.page_info_wrap{
    background: #EEE;
    padding : 10px;
    margin-top : 20px;
}
</style>
<!-- -->
<script>
import {Mixin} from '../../mixin'
import FlashMessage from '../../components/Layouts/FlashMessage'
import Dexie from 'dexie';
import LibDexie from '@/libs/LibDexie';

var db = null;
//
export default {
    mixins:[Mixin],
    components: { FlashMessage },
    created () {
        db = new Dexie( this.sysConst.DEXIE_DB_NAME );
        db.version(this.sysConst.DEXIE_DB_VERSION).stores(
                this.sysConst.DEXIE_DB_STORE );        
        this.get_items()
    },
    data () {
        return {
            tasks: [],
            key_name : "tasks",
        }
    },
    methods: {
        get_items(){
            var self = this
            db.tasks.toArray().then(function (items ) {
                self.tasks = LibDexie.get_reverse_items(items)
                //console.log( items )
            });
        },        
    }
}
</script>

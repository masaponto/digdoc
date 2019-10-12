<template>
    <div id="app">
        <div class="Title">
            <h1>Dig Doc</h1>
        </div>
        <div class="Input">
            <input type="text" v-model="keyword">
        </div>
        <div class="DocTable">
            <table align="center">
                <thead>
                    <tr>
                        <th v-for="(value, index) in columns" :key="index">
                            {{value}}
                        </th>
                    </tr>
                </thead>
                <tbody>
                    <tr v-for="(doc, index) in filterdDocs" :key="index">
                        <td v-text="doc.id"></td>
                        <td v-text="doc.name"></td>
                        <td v-text="doc.url"></td>
                        <td v-text="doc.note"></td>
                        <td v-text="doc.update"></td>
                    </tr>
                </tbody>
            </table>
        </div>
    </div>
</template>

<script>
 import docsMaster from "../assets/docs.json"

 export default {
     data: function(){
         return {
             keyword: '',
             docs: docsMaster,
             columns: ["id", "ファイル名", "URL", "備考", "最終更新"]
         }
     },
     computed: {
         filterdDocs: function() {
             let docs = this.docs;
             let keyword = this.keyword;
             if(keyword) {
                 docs = docs.filter(function(doc) {
                     return doc.name.indexOf(keyword) !== -1;
                 });
             }
             return docs;
         }
     }
 }
</script>

<style>
 table {
     border: 2px solid #42b983;
     border-radius: 3px;
     background-color: #fff;
 }
 th {
     background-color: #42b983;
     color: rgba(255,255,255,0.66);
     cursor: pointer;
     -webkit-user-select: none;
     -moz-user-select: none;
     -ms-user-select: none;
     user-select: none;
 }
 td {
     background-color: #f9f9f9;
 }
 th, td {
     min-width: 30px;
     padding: 10px 20px;
 }
 th.active {
     color: #fff;
 }
 th.active .arrow {
     opacity: 1;
 }

 input {
     margin-bottom: 10px;
 }

</style>

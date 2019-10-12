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
                <tr v-for="(doc, index) in filterdDocs" :key="index">
                    <td v-text="doc.id"></td>
                    <td v-text="doc.name"></td>
                    <td v-text="doc.url"></td>
                    <td v-text="doc.update"></td>
                    <td v-text="doc.note"></td>
                </tr>
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
             docs: docsMaster
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
</style>

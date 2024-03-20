<template>
    <div class="card-body">
        <h1>Merci</h1>
       
        <table class="min-w-full divide-y divide-gray-200 border">
            <thead>
                <tr>
                    <th class="px-6 py-3 bg-gray-50 text-left">
                        <span class="text-xs leading-4 font-medium text-gray-500 uppercase tracking-wider">ID</span>
                    </th>
                    <th class="px-6 py-3 bg-gray-50 text-left">
                        <span class="text-xs leading-4 font-medium text-gray-500 uppercase tracking-wider">Title</span>
                    </th>
                    <th class="px-6 py-3 bg-gray-50 text-left">
                        <span class="text-xs leading-4 font-medium text-gray-500 uppercase tracking-wider">Content</span>
                    </th>
                    <th class="px-6 py-3 bg-gray-50 text-left">
                        <span class="text-xs leading-4 font-medium text-gray-500 uppercase tracking-wider">Action</span>
                    </th>
                </tr>
            </thead>

            <tbody class="bg-white divide-y divide-gray-200 divide-solid">
                <tr v-for="article in articles" :key="article.id">
                    <td class="px-6 py-4 whitespace-no-wrap text-sm leading-5 text-gray-900">
                        {{ article.id }}
                    </td>
                    <td class="px-6 py-4 whitespace-no-wrap text-sm leading-5 text-gray-900">
                        {{ article.title }}
                    </td>
                    <td class="px-6 py-4 whitespace-no-wrap text-sm leading-5 text-gray-900">
                        {{ article.body }}
                    </td>
                 

                    <td class="px-6 py-4 whitespace-no-wrap text-sm leading-5 text-gray-900">
                        <router-link :to='{name:"articleEdit",params:{id:article.id}}' class="btn btn-success">Edit</router-link>

                   
                       <button type="button" @click="deleteArticle(article.id)" class="btn btn-danger">Delete</button>
                    </td>
                </tr> 
            </tbody>
        </table>
    </div>
</template>

<script>
import axios from 'axios';

export default {
    data() {
        return {
            articles: [],
        };
    },
    mounted() {
        this.fetchData();
    },
    methods: {
        fetchData() {
            axios.get('/api/articles')
                .then(response => { this.articles = response.data })
                .catch(error => { console.error('Error fetching data:', error) });
        },

        deleteArticle(id){
              if(confirm("Are you sure to delete this article")){
this.axios.delete(`/api/articles/${id}`)
.then(response => { this.fetchData()})
.catch(error => {console.log(error) })


              }


        }


    }
}

</script>




<style>
@import "resources/css/app.css";

</style>
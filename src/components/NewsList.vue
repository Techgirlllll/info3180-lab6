

<template>

<div class = "propRow">
    <div v-for="article in articles" class="card">
        <img class="propertyPict" v-bind:src="article.urlToImage" :alt="article.title" />
        <div class="card-body">
            <h5>{{ article.title }}</h5>
            <p class= "artDesc"> {{ article.description }}</p>
        </div>
    </div>
</div>
</template>


<script>
export default {
 data() {
 return {
     articles: []
 };
 },
 created() {
    let self = this;
    fetch(`https://newsapi.org/v2/top-headlines?country=us&apiKey=${import.meta.env.VITE_NEWSAPI_TOKEN}`,
    
{
 headers: {
    Authorization: `Bearer ${import.meta.env.VITE_NEWSAPI_TOKEN}`
 }
})
        .then(function(response) {
        return response.json();
 })
         .then(function(data) {
         console.log(data);
         self.articles = data.articles;
         });
    }
};

</script>

<style> 

.propRow {
    display: grid;
    grid-template-columns: repeat(3,1fr);
    gap: 60px;
}

.card {
    box-shadow: 0 10px 2px -2px #4CAF50;
}

.propertyPict {
    width:max-width;
    height: 300px;
}
</style>
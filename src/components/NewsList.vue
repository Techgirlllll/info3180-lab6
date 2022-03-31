

<template>

<form @submit.prevent="searchNews" class="d-flex flex-column justify-content-center">
    <div class="input-group mx-sm-3 mb-2">
        <label class="visually-hidden" for="search">Search</label>
        <input type="search" name="search" v-model="searchTerm" 
         id="search" class="form-control mb-2 mr-sm-2" placeholder="Enter search term here" />
        <button class="btn btn-primary mb-2">Search</button>
    </div>
    <p class="search">You are searching for {{ searchTerm }}</p>
 </form>

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
     articles: [],
     searchTerm: ' '
     }
 },
 methods: {
 searchNews() {
        let self = this;
            fetch('https://newsapi.org/v2/everything?q='+self.searchTerm + '&language=en', {
            headers: {
        'Authorization': `Bearer ${import.meta.env.VITE_NEWSAPI_TOKEN}`,
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
  }
};
</script>

<style> 

.propRow {
    display: grid;
    grid-template-columns: repeat(3,1fr);
    gap: 50px;
}
.search {
    font-weight: bold;
    margin-bottom: 5%;
    margin-left: 1%;
}

h2 {
    margin-left: 1%;
}

.card {
    box-shadow: 0 10px 2px -2px #4CAF50;
    transition: width 2s;
}
.card:hover{
    transform: scale(1.1);
    transition: all 1s ease;
}
.propertyPict {
    width:max-width;
    height: 300px;
}

</style>
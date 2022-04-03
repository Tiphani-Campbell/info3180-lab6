<template>
    <ul class="news__list">
        <li v-for="article in articles" class="news__item">  <br> <img :src="article.urlToImage" class="article-image"/> <br> <h4> {{ article.title }} </h4> <br> <p> {{ article.description }}</p></li>
    </ul>
</template>

<script>
export default{
    data() {
        return {
            articles: []
        }
    },
    created(){
        let self = this;
        fetch('https://newsapi.org/v2/top-headlines?country=us',
        {
            headers: {
                'Authorization' : `Bearer ${import.meta.env.VITE_NEWSAPI_TOKEN}`
            }
        })
        
        .then(function(response){
            return response.json();
        })

        .then(function(data){
            console.log(data);
            self.articles = data.articles;
        });
    }
}
</script>
<style>
    body{
      padding-top: 5rem;  
    }
    .news__list{
        display: grid;
        grid-template-columns: repeat(3, 1fr);
        list-style-type: none;
        grid-gap: 16px;
        
    }
    .article-image{
        width: 400px;
        border-top-left-radius: 5px;
        border-top-right-radius: 5px;
        
    }
    .news__item{
        display: grid;
        grid-template-rows: 1px auto;
        border-bottom: 5px solid rgb(14, 207, 159);
        border-radius: 5px;
        box-shadow:0 4px 8px rgba(0,0,0,0.2);
    }
    h4{
        padding: 10px;
        text-align: justify;
    }

    p{
        padding: 10px;
        text-align: justify;
    }

    
</style>
<template>
  <div>
    <div>
        <h1 style="margin-top: 5%; margin-bottom: 3%">News.</h1>
        <div class="row">
            <div v-for="article in articles" class="col-md-3" style="margin-right: 5%; margin-bottom: 5%">
                <b-card :title="article.title"
                      :img-src="article.urlToImage"
                      img-alt="Image"
                      img-top
                      tag="article"
                      class="mb-2 h-100">
                    <p class="card-text">
                      {{truncate(article.description)}}
                    </p>
                    <a :href="article.url" target="_blank" class="card-link">Read Full Story</a>
                </b-card>
            </div>
        </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios'
import Truncate from 'truncate'
export default {
    data: function() {
        return {
            articles: {}
        }
    },
    methods: {
        loadArticles: function() {
            var url = 'https://newsapi.org/v2/top-headlines?country=gb&apiKey='+'YOUR_KEY_HERE'

            axios.get(url).then(response => {
                this.articles = response.data.articles
            })
        },
        truncate: function(description) {
            return Truncate(description, 100)
        }
    },
    mounted() {
        this.loadArticles()
    }
}
</script>

<style media="screen">
    .custom_button {
        background-color: transparent;
        border: 0px solid;
        color: grey;
        outline: none;
    }
    .custom_button:hover {
        background-color: transparent;
        border: 0px solid;
        color: grey
    }
    .custom_button:focus {
        outline: none;
        border: 0px solid;
    }
    .btn:focus {
        outline: 0;
    }
</style>

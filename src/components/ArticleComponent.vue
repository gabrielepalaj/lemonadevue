<template>
    <div class="article">
      <img :src="article.imageUrl" alt="Immagine Articolo">
      <div class="title">{{ article.title }}</div>
    </div>
  </template>
  
  <script>
  export default {
    name: 'ArticleComponent',
    props: {
      article: {
        type: Object,
        required: true
      }
    }
  }
  </script>
  
  <style scoped>
  .article {
    display: flex;
    flex-direction: column;
    align-items: center;
    margin-bottom: 20px;
  }
  
  img {
    width: 100%;
    max-width: 200px;
    height: auto;
  }
  
  .title {
    margin-top: 10px;
    font-weight: bold;
  }
  </style>
  
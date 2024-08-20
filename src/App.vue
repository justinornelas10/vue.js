<script setup>
import { onMounted, ref } from "vue";
import BlogPost from "./components/BlogPost.vue";
import PaginatePost from "./components/PaginatePost.vue";
import LoadingSpinner from "./components/loadingSpinner.vue";

const posts = ref([]);
const favorite = ref("");

const postXpage = 10;
const start = ref(0);
const end = ref(postXpage);
const loading = ref(false)

const changeFav = (post) => {
  favorite.value = post;
};

// onMounted(async() => {
//   loading.value = true
//   try {
//     const res = await fetch("https://jsonplaceholder.typicode.com/posts")
//     posts.value = await res.json()
//   } catch (error) {
//     console.log(error)
//   }finally{
//     loading.value = false
//   }
// })

  // fetch("https://jsonplaceholder.typicode.com/posts")
  // .then((res) => res.json())
  // .then((data) => (posts.value = data))
  // .finally(() => (loading.value = false))

const fetchData = async () => {
  loading.value = true
  try {
    const res = await fetch("https://jsonplaceholder.typicode.com/posts")
    posts.value = await res.json()
  } catch (error) {
    console.log(error)
  }finally{
    loading.value = false
  }
}

fetchData()
const next = () => {
  start.value += postXpage;
  end.value += postXpage;
};

const prev = () => {
  start.value -= postXpage;
  end.value -= postXpage;
};
</script>

<template>
  <LoadingSpinner v-if="loading"/>

  <div class="container" v-else>
    <h1>APP's</h1>
    <h2>Mis post favoritos: {{ favorite }}</h2>

    <PaginatePost
      @next="next"
      @prev="prev"
      :start="start"
      :end="end"
      :maxLength="posts.length"
      class="w-auto d-flex p-3"
    >
    </PaginatePost>

    <BlogPost
      v-for="post in posts.slice(start, end)"
      :key="post.id"
      :title="post.title"
      :id="post.id"
      :body="post.body"
      :changeFav="changeFav"
    >
    </BlogPost>
  </div>
</template>

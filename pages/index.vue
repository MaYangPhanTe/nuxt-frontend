<template>
  <div>
    <h1>Posts</h1>
    <ul>
      <li v-for="post in posts" :key="post.id">
        {{ post.title }}
        <button @click="editPost(post.id)">Edit</button>
      </li>
    </ul>
  </div>
</template>

<script setup>
const config = useRuntimeConfig();
const { data: posts } = await useAsyncData("posts", () =>
  $fetch(`${config.public.apiBase}/posts`)
);

const router = useRouter();

const editPost = (id) => {
  router.push(`/edit/${id}`);
};
</script>

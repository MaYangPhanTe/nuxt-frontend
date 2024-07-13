<template>
  <div>
    <h1>Create Post</h1>
    <form @submit.prevent="createPost">
      <input v-model="title" placeholder="Title" />
      <textarea v-model="content" placeholder="Content"></textarea>
      <button type="submit">Create</button>
    </form>
  </div>
</template>

<script setup>
import { ref } from "vue";
import { useRouter } from "vue-router";

const title = ref("");
const content = ref("");
const router = useRouter();
const config = useRuntimeConfig();

const createPost = async () => {
  await $fetch(`${config.public.apiBase}/posts`, {
    method: "POST",
    body: { title: title.value, content: content.value },
  });
  router.push("/");
};
</script>

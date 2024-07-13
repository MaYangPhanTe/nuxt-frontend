<template>
  <div>
    <h1>Edit Post</h1>
    <form @submit.prevent="updatePost">
      <input v-model="title" placeholder="Title" />
      <textarea v-model="content" placeholder="Content"></textarea>
      <button type="submit">Update</button>
    </form>
  </div>
</template>

<script setup>
import { ref, onMounted } from "vue";
import { useRouter, useRoute } from "vue-router";

const title = ref("");
const content = ref("");
const router = useRouter();
const route = useRoute();
const config = useRuntimeConfig();

const fetchPost = async () => {
  const { data: post } = await useAsyncData(`post-${route.params.id}`, () =>
    $fetch(`${config.public.apiBase}/posts/${route.params.id}`)
  );
  title.value = post.value.title;
  content.value = post.value.content;
};

onMounted(fetchPost);

const updatePost = async () => {
  await $fetch(`${config.public.apiBase}/posts/${route.params.id}`, {
    method: "PUT",
    body: { title: title.value, content: content.value },
  });
  router.push("/");
};
</script>

<template>
  <div>
    <router-link class="routerBtn" :to=adress> {{ text }}</router-link>
  </div>
</template>

<script>
export default {
    name: 'RouteBtn',
    props: {
        adress: String,
        text: String
  },
}
</script>
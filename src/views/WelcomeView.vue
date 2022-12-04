<template>
  <div class="container">
    <h1>Calcula el teu pressupost!</h1>
    <h3>
      Amb aquesta aplicació podràs calcular el preu del servei que vols
      contractar.
    </h3>
    <RouteBtn :adress="`/home`" :text="`Calcula el pressupost`"/>
  </div>
</template>

<script>
import RouteBtn from '@/components/RouteBtn'

export default {
  name: 'WelcomeView',
  components: {
    RouteBtn
  },
}
</script>

<style scoped>
.container {
  margin: 0 auto;
  display: flex;
  flex-direction: column;
  align-items: center;
  width: 80vw;
}
h1 {
  margin: 40px;
}
h3 {
  margin-bottom: 40px;
  text-align: center;
}
</style>

<template>
  <main>
    <Header />

    <div class="homeContent">

      <div class="equipment">
        <div class="equipmentContent">
          <h2 class="name">Name</h2>
          <p class="description">descricao</p>

        </div>
      </div>
    </div>
  </main>
</template>



<script>
import axios from 'axios'
export default {
  name: 'home',
  components: 'Header',
  data() {
    return {
      equipments: [],
    }
  },
  methods: {
    getDevices: async function () {
      await axios.get(this.$store.state.BASE_URL + '/devices/')
        .then((response) => {
          let data = response.data
          this.equipments = data;
          // console.log(this.equipments);
        })
        .catch((err) => {
          console.log(err);
        })
    },
  },
  mounted: async function () {
    this.getDevices();
  }
}
</script>

<style lang="scss" scoped>
main {}
</style>
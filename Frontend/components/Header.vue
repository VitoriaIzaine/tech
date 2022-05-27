<template>
  <div>
    <div class="header flexRowSpaced">
      <img src="techman.png" alt="" class="logo" />
      <div class="headerContent flexRowRight">
        <a  @click="ModalCadastro = true">Novo Equipamento</a>
        <img src="logout_sair.png" alt="" class="logout" @click="goBack()"/>
      </div>
    </div>
    <Modal
        v-show="ModalCadastro"
        @close-modal="ModalCadastro = false"
      />
  </div>
</template>

<script>
export default {
    name: "Header",
    data() {
        return {
            ModalCadastro:false,
        };
    },
    methods: {
        goBack() {
            this.$router.back();
        }
    },
};
</script>

<style lang="scss" scoped>
.header {
  height: 75px;
  width: 100%;
  padding: 0 5px;
  background-color: var(--background);
  -webkit-box-shadow: 0px 0px 11px 0px rgba(0, 0, 0, 0.78);
  box-shadow: 0px 0px 11px 0px rgba(0, 0, 0, 0.78);
  img {
    height: 70px;
    width: 400px;
    margin-top: 5px;
  }
  .headerContent {
    padding-right: 15px;
    p {
      width: auto;
      height: auto;
      color: var(--dark);
      font-weight: bold;
      font-size: 20px;
      margin-right: 30px;
    }
    .logout {
      height: 30px;
      width: 30px;
      cursor: pointer;
    }
  }
a{
    cursor: pointer;
}
}
</style>
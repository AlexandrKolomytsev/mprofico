<template>
  <div>
    <div class="profile-nav">
      <div class="profile-nav__container">
        <p class="profile-nav__position">{{userData.position}}</p>
        <p class="profile-nav__name">{{userData.name}}</p>
      </div>
      <div class="nav__profile-photo">
        <img src="@/assets/img/user-photo.svg" alt="Фото пользоавтеля">
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "HeaderTab",
  data(){
    return{
      userData: {},
    }
  },
  mounted() {
    this.getDate()
  },
  methods: {
    getDate(){
      let raw = localStorage.getItem('userData')
      this.userData = JSON.parse(raw)
    }
  }
}
</script>

<style lang="scss" scoped>
.profile-nav{
  display: flex;
  gap: 25px;
  &__name{
    margin: 5px 11px 0 0;
    position: relative;
    text-align: right;
    &:after{
      content: "";
      position: absolute;
      top: 5px;
      right: -14px;
      display: block;
      width: 5px;
      height: 5px;
      border-top: 2px solid #322633;
      border-right: 2px solid #322633;
      transform: rotate(135deg);
    }
  }
}
</style>

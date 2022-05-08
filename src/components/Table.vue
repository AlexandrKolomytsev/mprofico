<template>
  <div class="container">
    <div class="table-wrapper">
      <table class="table">
        <thead class="table__header">
          <tr class="table__header-line">
            <th class="table__title">Компания</th>
            <th class="table__title">Новые заявки</th>
            <th class="table__title">
              Предварительные
              <div class="table__flex">
                <p class="table__subtitle">Актуальные</p>
                <p class="table__subtitle">Просроченные</p>
              </div>
            </th>
            <th class="table__title">
              Периодические
              <div class="table__flex">
                <p class="table__subtitle">Актуальные</p>
                <p class="table__subtitle">Просроченные</p>
              </div>
            </th>
            <th class="table__title">Вакцинация</th>
            <th class="table__title">Истекающие</th>
            <th class="table__title">Сотрудники</th>
            <th class="table__title">Завершенные</th>
          </tr>
          <div class="table-header-background"></div>
        </thead>
        <tbody class="table__body">
        <tr v-for="item in allDate" :key="item.id" class="table__body-line">
          <td>
            <img class="table__body-logo" :src="item.company" alt="Лого">
          </td>
          <td> <p class="table__body-border">{{ item.newApplications }}</p></td>
          <td>
            <div class="table__flex-body">
              <p class="table__body-border">{{ item.preliminaryCurrent }}</p>
              <p class="table__body-border">{{ item.preliminaryOverdue }}</p>
            </div>
          </td>
          <td>
            <div class="table__flex-body">
              <p class="table__body-border">{{ item.periodicCurrent }}</p>
              <p class="table__body-border">{{ item.periodicOverdue }}</p>
            </div>
          </td>
          <td><p class="table__body-border">{{ item.vaccination }}</p></td>
          <td><p class="table__body-border">{{ item.expiring }}</p></td>
          <td><p class="table__body-border info">{{ item.employee }}</p></td>
          <td><p class="table__body-border info">{{ item.completed }}</p></td>
        </tr>
        </tbody>
      </table>
    </div>
    <div class="img-block">
      <img src="@/assets/img/company-logo1.png" alt="Лого">
      <img src="@/assets/img/company-logo2.png" alt="Лого">
      <img src="@/assets/img/company-logo3.png" alt="Лого">
      <img src="@/assets/img/company-logo4.png" alt="Лого">
      <img src="@/assets/img/company-logo5.png" alt="Лого">
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "Table",
  data () {
    return {
      allDate: '',
      accessibleDate: '',
      role: ''
    }
  },
  mounted() {
    this.getDate()
    this.getIncidents()
  },
  methods: {
    async getIncidents () {
      this.allDate = await axios.get('http://localhost:3001/applications').then(res => res.data)
      if (this.role === 'role-one'){
        this.accessibleDate = this.allDate.splice(3)
        console.log(this.allDate.splice(3))
      }
    },
    getDate(){
      let raw = localStorage.getItem('userData')
      this.userData = JSON.parse(raw)
      this.role = this.userData.role
    }
  }

}
</script>

<style lang="scss" scoped>
.table{
  width: 100%;
  border-collapse: collapse;
  &__flex{
    display: flex;
    justify-content: space-around;
    gap: 35px;
    margin-top: 5px;
  }
  &__header{
    /*background-color: #E5E5E5;
    border-radius: 10px;*/
    position: relative;
    z-index: 1;
  }
  &__header-line{
    background: transparent;
  }
  &__title{
    font-weight: 700;
    font-size: 14px;
    line-height: 19px;
    color: #757C93;
  }
  &__subtitle{
    font-weight: 400;
    font-size: 14px;
    line-height: 19px;
    text-align: center;
    color: #757C93;
  }
  &__flex-body{
    display: flex;
    gap: 54px;
  }
  &__body-line{
    height: 100px;
  }
  &__body-border{
    padding: 10px;
    background: #7A49A3;
    border-radius: 5px;
    color: #FFFFFF;
    width: fit-content;
    margin: 0 auto;
  }
  & .info{
    color: #322633;
    background: transparent;
    font-style: normal;
    font-weight: 700;
    font-size: 14px;
    line-height: 19px;
  }
  & .disable{
    background: #E2E2E2;
  }
  &__body-logo{
    width: 95px;
    display: flex;
    margin: 0 auto;
  }
}
.table-wrapper{
  background-color: #FFFFFF;
  border-radius: 20px;
  margin: 70px 0;
  padding: 30px 27px 30px 32px;
  & .table-header-background{
    position: absolute;
    width: 100%;
    height: 63px;
    background-color: #F6F5F8;
    border-radius: 10px;
    top: -8px;
    left: 0;
    z-index: -1;
  }
}
.img-block{
  display: none;
}
</style>

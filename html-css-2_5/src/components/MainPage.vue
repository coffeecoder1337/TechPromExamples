<template>
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Raleway:wght@100&display=swap" rel="stylesheet">
  <div class="header-background-img" style="overflow-x: hidden">
    <header>

      <button class="text-center main_button">VELES</button>

      <nav>
        <div class="topnav" id="myTopnav">
          <router-link to="" class="router-link-text">Земля</router-link>
          <router-link to="" class="router-link-text">Крановые площадки</router-link>
          <router-link to="" class="router-link-text">Выгрузка вагонов</router-link>
          <router-link to="" class="router-link-text">Фасовка</router-link>
          <router-link to="" class="router-link-text">Щебень</router-link>
          <router-link to="" class="resp-false"><img src="/mini-phone.png" alt="">+7 (927) 678-45-14</router-link>
          <router-link to="" class="resp-false" style="font-size: 10px; letter-spacing: 0"><img src="/geoposition.png" alt="">г.Казань, Складская 20</router-link>
          <router-link to="" @click="openMenu" class="router-link-text icon">&#9776;</router-link>
          <router-link to="" @click="openMenu" class="router-link-text icon-resp">&#10005;</router-link>
        </div>
      </nav>

    </header>

    <div class="main-div">

      <div>
        <h1 class="main-text">выгрузка вагонов, аренда земли, крановых площадок, ответственное хранение</h1>
        <button class="button-get">заказать</button>
      </div>

      <img src="/main-header.png" class="prewiew-img" alt="">

      <div class="navigate-buttons">
        <button class="img-button" @click="slideRed">&larr;</button>
        <p class="what-slide-text">{{whatSlide}} / 3</p>
        <button class="img-button" @click="slideInc">&rarr;</button>
      </div>
    </div>
  </div>


  <div style="background-color: #F1F2F5">
    <h1 class="second-h1">Чем мы можем быть полезны?</h1>
    <div class="container main-container">
      <div class="row row-cols-1 row-cols-md-2 row-cols-lg-3">
        <div class="col" v-for="blockData in blocksData" :key="blockData.id">
          <div class="card card-data" @mouseover="blockData.upHere = true" @mouseleave="blockData.upHere = false" :class="{active: blockData.upHere}">
            <div v-if="blockData.mapsLink" class="map-div">
              <img src="/card-position.png" alt="" class="map-div-img">
              <p class="map-div-text">Смотреть карту территорий</p>
            </div>
            <img :src="blockData.img" class="card-img-top" style="border-radius: 0 !important;" alt="...">
            <div class="card-body">
              <p class="card-title card-title-edit">{{ blockData.text }}</p>
            </div>


          </div>
        </div>
      </div>
    </div>
  </div>

  <div class="advantages">
    <h1 class="rd-h1">Наши преимущества</h1>
    <div class="container main-container">
      <div class="row row-cols-1 row-cols-md-2 row-cols-lg-3">

        <div class="col advantages-div" v-for="advantage in advantages" :key="advantage.id">
          <p class="number-advantage">{{advantage.number}}</p>
          <p class="description-advantage">{{advantage.text}}</p>
        </div>

      </div>
    </div>
  </div>

  <div class="get-margin">

    <div class="container main-container get-consultation-main-div">
      <h1 class="rd-h1">Карта территорий</h1>
      <img src="/map.png" alt="" style="margin-top: 45px; width: 100%">
    </div>

    <div class="container main-container get-consultation-align">

      <div>
        <img src="/left-placed-picture.png" alt="" class="get-consultation-img">
      </div>

      <div class="get-consultation-div">
        <h1 class="get-consultation-h">АРЕНДА ЗЕМЛИ</h1>
        <p class="fouth-container-text">Предлагаем в аренду открытые площадки для хранения грузов и техники. Площадь базы составляет 11,5га. Общая протяженность внутренних ж/д путей позволяет производить погрузо-разгрузочные работы до 60 вагонов в сутки единовременно. На базе работают два маневровых собственных тепловоза. Есть железнодорожные и автомобильные весы, козловой кран, повышенный путь, пандусы для выгрузки крытых вагонов и фур.</p>
        <button class="get-consultation-button">
          ПОЛУЧИТЬ КОНСУЛЬТАЦИЮ
        </button>
      </div>

    </div>

  </div>


  <div class="main-div-last" style="margin-bottom: 200px">

    <img src="/last_photo.png" class="last-img" alt="">

    <div class="last">
      <h1 class="main-text-last">АРЕНДА СКЛАДОВ</h1>
      <p class="text-last">Предлагаем в аренду крытые и открытые складские и производственные площадки. Склады комплекса оснащены погрузочно-разгрузочной техникой. Открытые складские площадки приспособлены и для хранения негабаритных грузов. Собственный ж.д. подъездной путь. Охраняемая территория, удобные подъездные пути для любых видов транспорта. На закрытой территории базы обеспечивается функционирование всех инженерных сетей.</p>
      <button class="get-consultation-button-last">ПОЛУЧИТЬ КОНСУЛЬТАЦИЮ</button>
    </div>

  </div>


  <div class="input-div">
    <h1 class="input-h">
      УЗНАТЬ О ЦЕНАХ, ПОЛУЧИТЬ КОНСУЛЬТАЦИЮ ИЛИ ПЕРСОНАЛЬНОЕ ПРЕДЛОЖЕНИЕ
    </h1>

    <div class="container full">
      <div class="row row-cols-lg-3">

        <div class="row input-area">
          <input type="text" value="Имя">
        </div>

        <div class="row input-area">
          <input type="text" value="Телефон">
        </div>

        <div class="row fixing">
          <button class="last-input-button">ОТПРАВИТЬ</button>
        </div>

      </div>
    </div>
  </div>


  <footer class="footer-style" style="overflow-x: hidden">

    <button class="main_buttonFooter">VELES</button>

    <nav>
      <div class="topnavFooter responsive" id="myTopnav">
        <router-link to="" class="router-link-text">Земля</router-link>
        <router-link to="" class="router-link-text">Крановые площадки</router-link>
        <router-link to="" class="router-link-text">Выгрузка вагонов</router-link>
        <router-link to="" class="router-link-text">Фасовка</router-link>
        <router-link to="" class="router-link-text">Щебень</router-link>
        <router-link to="" class="resp-false"><img src="/mini-phone.png" alt="">+7 (927) 678-45-14</router-link>
        <router-link to="" class="resp-false" style="font-size: 10px; letter-spacing: 0"><img src="/geoposition.png" alt="">г.Казань, Складская 20</router-link>
      </div>
    </nav>

  </footer>
</template>

<script>
export default{
  data(){
    return{
      whatSlide: 1,
      blocksData: [
        {id: 1, img: 'img_0.png', text: 'крановая площадка', maps: '', mapsLink:'geo', upHere: false},
        {id: 2, img: 'img_1.png', text: 'товары сельского зозяйства', maps: '', mapsLink:'', upHere: false},
        {id: 3, img: 'img_2.png', text: 'фасовка от 300 гр до 1 тонны', maps: '', mapsLink:'', upHere: false},
        {id: 4, img: 'img_3.png', text: 'гранитный щебень', maps: '', mapsLink:'', upHere: false},
        {id: 5, img: 'img_4.png', text: 'аренда земли', maps: '', mapsLink:'geo', upHere: false},
        {id: 6, img: 'img_5.png', text: 'аренда складов', maps: '', mapsLink:'', upHere: false},
        {id: 7, img: 'img_6.png', text: 'выгрузка вагонов и ответственное хранение', maps: '', mapsLink:'', upHere: false},
        {id: 8, img: 'img_7.png', text: 'автономные весы 18м, 80т', maps: '', mapsLink:'geo', upHere: false},
        {id: 9, img: 'img_8.png', text: 'железнодорожные весы на 2 вагона', maps: '', mapsLink:'', upHere: false},
      ],
      advantages: [
        {id: 1, number: '01', text: '11,5 га площадь базы'},
        {id: 2, number: '02', text: '2 своих тепловоза'},
        {id: 3, number: '03', text: 'Повышенный путь для выгрузки инертных грузов'},
        {id: 4, number: '04', text: '8 км от центра Казани'},
        {id: 5, number: '05', text: 'Возможность выгрузки хопров и сыпучих грузов'},
        {id: 6, number: '06', text: 'Железнодорожные весы на 2 вагона'},
        {id: 7, number: '07', text: 'Автомобильные весы 18 м на 80 тонн'},
        {id: 8, number: '08', text: '3 пандуса для выгрузки и загрузки крытых вагонов и фур'},
        {id: 9, number: '09', text: 'Козловой кран'},
      ]
    }
  },
  methods: {
    slideInc(){
      if (this.whatSlide === 3){
        return this.whatSlide = 1
      }
      else{
        return this.whatSlide += 1
      }
    },
    slideRed(){
      if (this.whatSlide === 1){
        return this.whatSlide = 3
      }
      else{
        return this.whatSlide -= 1
      }
    },
    openMenu() {
      let x = document.getElementById('myTopnav')

      if (x.className === 'topnav') {
        return x.className += ' responsive'
      } else {
        return x.className = 'topnav'
      }
    }
  }
}

</script>

<style>
.last-input-button{
  margin-right: 7.5px;
  margin-left: 7.5px;
  color: #F1F2F5;
  background-color: #161616;
  border: none;
  font-family: 'Raleway', sans-serif;
  font-weight: bold;
  font-size: 12px;
  letter-spacing: 0.07vw;
  padding: 9px 20px 9px 20px;
  max-width: 170px;
  height: 50px;
}
.input-area{
  margin-right: 7.5px !important;
  margin-left: 7.5px !important;
  margin-bottom: 20px;
  font-family: 'Raleway', sans-serif;
  font-weight: lighter;
  font-size: 16px;
  height: 55px;
  width: 25% !important;
}
.input-div{
  max-width: 44%;
  margin-left: auto;
  margin-right: auto;
  margin-bottom: 100px;
}
.input-h{
  max-width: 90%;
  font-family: 'Raleway', sans-serif;
  font-weight: bold;
  font-size: 25px;
  letter-spacing: 0.13vw;
  text-align: center;
  margin-bottom: 30px;
}
.get-margin{
  margin-bottom: 100px;
}
.get-consultation-button-last{
  color: #F1F2F5;
  background-color: #161616;
  border-color: #F1F2F5;
  font-family: 'Raleway', sans-serif;
  font-weight: bold;
  font-size: 12px;
  letter-spacing: 0.02vw;
  padding: 12px 30px 11px 30px; 
}
.last{
  margin-left: 20%;
}
.last-img{
  position: absolute;
  right: 0;
  max-width: 50%;
  margin-top: 130px
}
.text-last{
  font-family: 'Raleway', sans-serif;
  font-weight: normal;
  font-size: 15px;
  color: #F1F2F5;
  margin-top: 30px;
  max-width: 33%;
}
.main-text-last{
  font-family: 'Raleway', sans-serif;
  font-weight: bolder;
  font-size: 30px;
  letter-spacing: 0.13vw;
  color: #F1F2F5;
  margin-top: 205px;
  max-width: 40%;
}
.main-div-last{
  height: 600px;
  display: flex;
  width: 100%;
  background-color: #161616;
}
.get-consultation-main-div{
  margin-bottom: 190px
}
.get-consultation-div{
  position: center;
  padding-right: 75px;
  width: 50%;
  margin-top: 100px
}
.get-consultation-img{
  width: 50%;
  float: right;
  margin-bottom: 100px;
  padding-left: 75px
}
.get-consultation-h{
  margin-bottom: 25px;
  font-family: 'Raleway', sans-serif;
  font-weight: bolder;
  font-size: 30px;
  letter-spacing: 0.13vw;
}
.get-consultation-button{
  color: #F1F2F5;
  background-color: #161616;
  font-family: 'Raleway', sans-serif;
  font-weight: bold;
  font-size: 12px;
  letter-spacing: 0.02vw;
  padding: 12px 30px 11px 30px;
}
.fouth-container-text{
  font-family: 'Raleway', sans-serif;
  font-weight: bold;
  font-size: 15px;
  color: #161616;
  margin-top: 25px;
  margin-bottom: 40px;
}
.map-div-text{
  display: none;
}
.map-div-img{
  height: 36px;
  width: 36px;
  position: absolute;
  left: 11px;
}
.map-div{
  position: absolute;
  width: 54px;
  height: 54px;
  background-color: #FFE500;
  display: inline-block;
  text-align: center;
  padding-top: 9px;
  padding-bottom: 9px
}
.rd-h1{
  padding-top: 100px;
  font-family: 'Raleway', sans-serif;
  font-weight: bolder;
  font-size: 30px;
  color: #161616;
  text-align: center;
}
.advantages-div{
  padding-top: 84px;
}
.description-advantage{
  vertical-align: top;
  display: inline-block;
  max-width: 50%;
  font-family: 'Raleway', sans-serif;
  font-weight: bolder;
  letter-spacing: 0;
  font-size: 16px;
}
.number-advantage{
  height: 51px;
  width: 51px;
  background-color: #FFE500;
  display: inline-block;
  text-align: center;
  padding-top: 10px;
  padding-bottom: 18px;
  margin-right: 40px;
  font-family: 'Raleway', sans-serif;
  font-weight: bolder;
  letter-spacing: 0.03vw;
  font-size: 20px;
}
.main-container{
  max-width: 62% !important;
}
header{
  min-height: 100px;
  background-color: #161616;
}
.footer-style{
  min-height: 100px;
  background-color: #161616;
}
.card-title-edit{
  font-family: 'Raleway', sans-serif;
  font-weight: bolder;
  letter-spacing: 0.03vw;
  font-size: 18px;
}
.card-data{
  margin: 25px 15px 45px 15px;
  border: none !important;
  border-radius: 0 !important;
  height: 460px !important;
  max-width: 370px;
  box-shadow: -5px 5px 5px 5px rgba(0, 0, 0, .07);
}
.card-data:hover{
  transform: translate(0, -20px);
}
.card-data:hover .map-div{
  width: 90%;
}
.card-data:hover .map-div-text{
  display: inline-block;
  margin-left: 30px;
  font-size: 14px;
}
.second-h1{
  padding-top: 12%;
  font-family: 'Raleway', sans-serif;
  font-weight: bolder;
  font-size: 30px;
  color: #161616;
  text-align: center;
}
.what-slide-text{
  display: inline-block;
  font-family: 'Raleway', sans-serif;
  font-size: 18px;
  color: #F1F2F5;
  background-color: transparent;
  margin: 20px;
}
.img-button{
  display: inline-block;
  color: #F1F2F5;
  background-color: transparent;
  border: none;
  transform: scaleX(2);
}
.navigate-buttons{
  position: absolute;
  margin-left: 37%;
  margin-top: 360px;
}
.prewiew-img{
  max-width: 50%;
  height: auto;
  position: absolute;
  right: 0;
  top: 178px;
}
.button-get{
  font-family: 'Raleway', sans-serif;
  font-weight: 900;
  font-size: 18px;
  letter-spacing: 0.13vw;
  color: #161616;
  background-color: #FFE500;
  max-height: 60px;
  margin-left: 27%;
  margin-top: 51px;
  border: 1px solid #FFE500;
  padding: 16px 53px 16px 53px;
}
.main-div{
  height: 450px;
  display: flex;
  width: 100%;
  background-color: #161616;
}
.main-text{
  font-family: 'Raleway', sans-serif;
  font-weight: bold;
  font-size: 27px;
  letter-spacing: 0.12vw;
  color: #F1F2F5;
  margin-left: 27%;
  margin-top: 130px;
  max-width: 40%;
}
header{
  width: 100%;
  display: flex;
}
footer{
  width: 100%;
  display: flex;
}
.icon-resp{
  display: none;
}
.resp-false{
  color: #F1F2F5;
  text-decoration: none;
  padding: 5px 15px;
}
.topnav{
  font-family: 'Raleway', sans-serif;
  font-size: 13px;
  width: 100%;
  letter-spacing: 0.1vw;
  margin-top: 40px;
  margin-left: 9%;
}
.topnavFooter{
  font-family: 'Raleway', sans-serif;
  font-size: 13px;
  width: 100%;
  letter-spacing: 0.1vw;
  margin-top: 40px;
  margin-left: 9%;
}
.topnav .icon{
  display: none;
}
.router-link-text{
  color: #F1F2F5;
  text-decoration: none;
  padding: 5px 15px;
}
.main_button{
  font-family: 'Raleway', sans-serif;
  font-size: 12px;
  letter-spacing: 0.22vw;
  border: 1px solid #F1F2F5;
  margin-left: 18%;
  margin-top: 30px;
  color: #F1F2F5;
  background-color: #161616;
  width: 91px;
  height: 36px
}
.main_buttonFooter{
  font-family: 'Raleway', sans-serif;
  font-size: 12px;
  letter-spacing: 0.22vw;
  border: 1px solid #F1F2F5;
  margin-left: 18%;
  margin-top: 30px;
  color: #F1F2F5;
  background-color: #161616;
  width: 91px;
  height: 36px
}@media screen and (max-width: 991px) {
  .input-h{
    margin-right: auto;
    margin-left: auto;
  }
  .fixing{
    margin: 0 !important;
  }
  .input-area{
    margin-right: auto !important;
    margin-left: auto !important;
    width: 100% !important;
  }
  .last-input-button{
    margin-right: auto !important;
    margin-left: auto !important;
    width: 100% !important;
  }
  .input-div {
    align-items: center;
  }
}
@media screen and (max-width: 1600px) {
  .input-div{
    max-width: 60%;
  }
  .card-data:hover .map-div-text {
    font-size: 10px;
  }
  .main-text-last{
    margin-top: 105px
  }
}
@media screen and (max-width: 1450px) {
  .router-link-text{
    color: #161616;
    font-weight: bold;
  }
  .resp-false{
    color: #161616;
    font-weight: bold;
  }
  .main_button{
    border-color: #161616;
    color: #161616;
    font-weight: bold;
  }
  .card-data:hover .map-div-text {
    font-size: 15px;
  }
  .main-container{
    max-width: 90% !important;
  }
  .header-background-img{
    background: linear-gradient(rgba(255, 255, 255, 0.001), rgba(0, 0, 0, 1.5)), url("../../public/main-header.png");
    background-repeat: no-repeat;
    background-position: center;
    background-size: cover;
  }
  .navigate-buttons{
    margin-left: 80%;
  }
  .img-button{
    transform: none;
  }
  header{
    background-color: transparent;
  }
  .main_button{
    background-color: transparent;
  }
  .main-div{
    background-color: transparent;
  }
  .prewiew-img{
    display: none;
  }
}
@media screen and (max-width: 1300px){
  .last{
    margin-left: 10%;
  }
  .main-container{
    max-width: 90% !important;
  }
  .topnav{
    letter-spacing: 0;
  }
  .topnavFooter{
    letter-spacing: 0;
  }
  .router-link-text{
    padding: 5px 8px;
  }
  nav{
    width: 100%;
    overflow:hidden;
  }
}
@media screen and (max-width: 410px){
  .main-div-last{
    margin-bottom: 60px !important
  }
  .input-div{
    margin-right: 0 !important;
    margin-left: 0 !important;
    width: 100% !important;
  }
  .last-input-button{
    margin-right: 0 !important;
    margin-left: 0 !important;
    width: 100% !important;
  }
  .get-margin{
    margin-bottom: 200px;
  }
  .main-div-last{
    height: 500px;
  }
  .fouth-container-text{
    margin-bottom: 30px;
  }
  .get-consultation-div p{
    font-size: 15px !important;
  }
  .get-consultation-div h1{
    font-size: 18px !important;
  }
  .get-consultation-button{
    font-size: 12px;
    letter-spacing: 0.02vw;
    position: absolute;
    width: 100%;
    height: 55px;
    left: 0;
    padding-left: 0;
    padding-right: 0;
  }
  .map-div-img{
    left: 7px;
  }
  .card-data{
    height: 370px !important;
    margin-right: 0;
    margin-left: 0 !important;
    width: 100%;
  }
  .card-data:hover .map-div-text {
    font-size: 10px !important;
    margin-left: 20px;
  }
  .navigate-buttons{
    margin-left: 60% !important;
    margin-top: 390px;
  }
  .img-button{
    transform: scaleX(0.5);
  }
  .what-slide-text{
     font-size: 10px;
   }
  .button-get{
    font-size: 14px;
    max-height: 55px;
    width: 120px !important;
    margin-left: 10%;
    margin-top: 36px;
    padding: 10px 20px 12px 20px;
  }
  .main-text{
    font-size: 18px;
    margin-left: 10%;
    margin-top: 100px !important;
    max-width: 70% !important;
  }
  .text-last{
    font-size: 13px !important;
  }
}
@media screen and (max-width: 675px){
  .input-div{
    width: 90%;
  }
  .input-area{
    width: 100% !important;
  }
  .get-consultation-main-div{
    margin-bottom: 50px;
  }
  .map-div-img{
    left: 6px;
  }
  .map-div-img{
    height: 18px;
    width: 18px;
  }
  .map-div{
    width: 30px;
    height: 30px;
    padding-top: 3px;
  }
  .navigate-buttons{
    margin-left: 75%;
    margin-top: 380px;
  }
  .what-slide-text{
    margin: 6px;
  }
  .button-get{
    font-size: 16px;
    max-height: 55px;
    max-width: 168px;
    margin-left: 10%;
    margin-top: 36px;
  }
  .main-text{
    margin-left: 10%;
    font-size: 22px;
    margin-top: 50px !important;
    max-width: 60%;
  }
  .card-data{
    margin: 25px 25% 45px 25%;
  }
}
@media screen and (max-width: 767px){
  .full{
    width: 100% !important;
    margin-right: auto !important;
    margin-left: auto !important;
  }
  .input-area{
    margin-right: auto !important;
    margin-left: auto !important;
  }
  .input-h{
    width: 100%;
    margin-right: auto;
    margin-left: auto
  }
  .input-div{
    max-width: 100%;
    width: 100%;
  }
  .main-div-last{
    height: 650px;
  }
  .text-last{
    max-width: 100% !important;
    margin-left: 5%;
    margin-right: 5%;
    display: block;
  }
  .last{
    margin-left: 0;
    text-align: center;
  }
  .main-text-last{
    display: block;
    max-width: 100% !important;
    margin-left: 5%;
    margin-right: 5%;
    margin-top: 50%;
  }
  .last-img{
    margin-top: -40px;
    left: 0;
    right: 0;
    margin-left: 5%;
    margin-right: 5%;
    max-width: 90%;
  }
  .get-consultation-align{
    text-align: center;
  }
  .get-consultation-img{
    float: none;
    width: 100%;
    margin-bottom: 18px;
    padding-left: 0 !important;
  }
  .get-consultation-div{
    padding: 0 !important;
    width: 100%;
    margin-top: 0;
  }
  .card-data{
    margin: 25px 25% 45px 25%;
  }
  .get-consultation-h{
    font-size: 30px;
  }
  .fouth-container-text{
    font-size: 15px;
  }
}
@media screen and (max-width: 1160px) {
  .input-area{
    width: 35%;
  }
  .card-data:hover .map-div-text {
    font-size: 15px;
  }
  .text-last{
    font-size: 12px;
    max-width: 40%;
  }
  .main-text-last{
    font-size: 22px;
    max-width: 40%;
  }
}
@media screen and (max-width: 1100px){
  .get-consultation-h{
    font-size: 22px;
  }
  .fouth-container-text{
    font-size: 12px;
  }
  .get-consultation-div{
    padding-right: 35px;
  }
  .get-consultation-img{
    padding-left: 35px;
  }
  .main-container{
    max-width: 90% !important;
  }
  .footer-style{
    display: flex;
    text-align: center
  }
  .router-link-text{
    display: none;
    color: #F1F2F5;
  }
  .topnav .icon{
    text-align: right;
    float: right;
    display: inline;
    color: #F1F2F5;
    margin-top: -20px;
    font-size: 24px;
    margin-right: 12%;
  }
  .topnav .icon-resp{
    display: none;
    text-align: right;
    float: right;
    color: #F1F2F5;
    margin-top: -20px;
    font-size: 24px;
    margin-right: 12%;
  }
  .main_button{
    margin-left: 10%;
  }
  .main_buttonFooter{
    margin-left: 0;
    margin-top: 5%;
  }
  nav{
    width: 100%;
    overflow:hidden;
  }
  .topnav.responsive{
    position: relative;
    top: 150px;
    left: -50%;
  }
  .topnavFooter.responsive{
    margin-top: 10%;
    margin-left: 0;
  }
  header .topnav.responsive{
    height: 568px;
  }
  footer{
    height: 568px;
  }
  .topnav.responsive .icon{
    display: none !important;
  }
  .topnav.responsive .icon-resp{
    position: absolute;
    top: -150px;
    bottom: 95px;
    right: -50%;
  }
  .topnav.responsive .router-link-text{
    letter-spacing: 0.12vw;
    padding-bottom: 39px;
    margin-left: 50%;
    float: none;
    display: block;
    text-align: center;
  }
  footer{
    display: block !important;
  }
  .topnavFooter.responsive .router-link-text{
    letter-spacing: 0.15vw;
    font-size: 20px;
    padding-bottom: 40px;
    display: block;
    text-align: center;
  }
  .resp-false{
    display: none;
    color: #F1F2F5;
  }
  .button-get{
    font-size: 16px;
    max-height: 55px;
    max-width: 168px;
    margin-left: 10%;
    margin-top: 36px;
  }
  .main-text{
    margin-left: 10%;
    margin-top: 100px;
    max-width: 40%;
  }
}
@media screen and (max-width: 665px){
  .card-data{
    margin-right: auto;
    margin-left: auto !important;
    width: 100%;
  }
  .router-link-text{
    display: none;
  }
  .topnav .icon{
    text-align: right;
    float: right;
    display: inline;
    color: #F1F2F5;
    margin-top: -20px;
    font-size: 24px;
    margin-right: 12%;
  }
  .topnav .icon-resp{
    display: none;
    text-align: right;
    float: right;
    color: #F1F2F5;
    margin-top: -20px;
    font-size: 24px;
    margin-right: 12%;
  }
  .main_button{
    margin-left: 10%;
  }
  .main_buttonFooter{
    margin-left: 0;
    margin-bottom: 10%;
    margin-top: 10%;
  }
  nav{
    width: 100%;
    overflow:hidden;
  }
  .topnav.responsive{
    position: relative;
    top: 150px;
    left: -50%;
  }
  .topnavFooter.responsive{
    margin-top: 10%;
    margin-left: 0;
  }
  header .topnav.responsive{
    height: 568px;
  }
  footer{
    height: 568px;
  }
  .topnav.responsive .icon{
    display: none !important;
  }
  .topnav.responsive .icon-resp{
    position: absolute;
    top: -150px;
    bottom: 95px;
    right: -50%;
  }
  .topnav.responsive .router-link-text{
    letter-spacing: 0.12vw;
    padding-bottom: 39px;
    margin-left: 50%;
    float: none;
    display: block;
    text-align: center;
  }
  footer{
    display: block !important;
  }
  .topnavFooter.responsive .router-link-text{
    letter-spacing: 0.12vw;
    font-size: 14px;
    padding-bottom: 40px;
    display: block;
    text-align: center;
  }
  .resp-false{
    display: none;
  }
}
</style>
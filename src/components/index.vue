<template>
  <div class="weather">
      <div class="content_top">
        <h1>{{WeatherData.weather}}</h1>
        <h2>{{CityData.province}} {{CityData.city}}</h2>
        <p>{{WeatherData.date |intercept}}</p>
        <img src="../../static/img/logo_e.png" width="100%" alt="">
      </div>
      <div class="content_bottom">
        <ul>
          <li v-for="(completes,index) in complete">
            <a @click="linkInfo(index)" class="Onetime active">
              <span>{{completes.date |intercepts}}</span>
              <span>{{completes.temperature}}</span>
            </a>
          </li>
        </ul>
      </div>
  </div>
</template>

<script>
export default {
  mounted(){
    this.GetUserIp()
  },
//  过滤器
  filters:{
    intercept(val){
      return val.slice(-3,-1)
    },
    intercepts(valu){
      return valu.slice(0,2)
    }
  },
  data(){
    return{
      CityData:{},
      complete:[],
      WeatherData:{
        weather:"",
        date:"",
      },
    }
  },
  methods: {
    linkInfo(id){
      localStorage.setItem("WeatherData",JSON.stringify(this.WeatherData.complete));
      this.$router.push({name:'Info',params:{ id: id}});
    },
//:to="{ name:'Info',params:{ id: index} }"
    GetUserIp(){
      this.$http.get(this.$config.GetUserIp)
      .then(success=>{
        console.log(success);
        this.GetUserAddress(success.data.ip);
      })
      .catch(error=>{
        $.toast("网络不好，稍后再试")
      })
    },
    GetUserAddress(ips){
      this.$http.jsonp(this.$config.GetUserAddress,{
        params:{
          ak:this.$config.IpConfig.ak,
          ip:ips
        }
      })
      .then(success=>{
        console.log(success);
        this.CityData=success.data.content.address_detail;
        this.GetUserWeather();
      })
      .catch(error=>{
        $.toast("网络不好，稍后再试")
      })
    },
    GetUserWeather(){
      this.$http.jsonp(this.$config.GetUserWeather,{
        params:{
          location:this.CityData.city,
          output:"json",
          ak:this.$config.IpConfig.ak,
        }
      })
      .then(success=>{
        console.log(success);
        this.WeatherData.weather=success.data.results[0].weather_data[0].weather;
        this.WeatherData.date=success.data.results[0].weather_data[0].date;
        this.complete=success.data.results[0].weather_data;
        console.log(this.complete);
      })
      .catch(error=>{
        $.toast("网络不好，稍后再试")
      })
    },
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  *{
    margin: 0;
    padding: 0;
    list-style: none;
  }
  .weather{
    text-align: center;
    height: 100%;
  }
  h1, h2 {
    font-size: 30px;
    font-weight: normal;
  }
  .content_top{
    padding-top: 100px;
    color: #fff;
    background: -webkit-linear-gradient(#dd4879 , #fdd73f);
    background: -o-linear-gradient(#dd4879 , #fdd73f);
    background: -moz-linear-gradient(#dd4879 , #fdd73f);
    background: linear-gradient(#dd4879 , #fdd73f);
    height: 80%;
    position: relative;
  }
  .content_top h1{
    font-weight: 500;
  }
  .content_top h2{
    font-size: 20px;
    font-weight: 400;
  }
  .content_top p{
    font-size: 80px;
  }
  .content_top img{
    margin-top: 98px;
    position: absolute;
    left: 0;
    bottom: 0;
  }
  .content_bottom ul li{
    border-bottom: 1px solid #ccc;
  }
  .content_bottom ul li a{
    overflow:hidden ;
    display: block;
    margin: 23px 30px;
    text-align: center;
  }
  .content_bottom ul li:first-child a{
    color: red;
  }
  .Onetime span:first-child{
    float: left;
  }
  .Onetime span:last-child{
    float: right;
  }
  .Towtime span:first-child{
    float: left;
  }
  .Towtime span:last-child{
    float: right;
  }
</style>

<template>
    <div class="info">
        <div class="info-top">
          <div class="row info-top-city">
            <div class="col-50 info-top-left">
              <span>天气</span>
            </div>
            <div class="col-50 info-top-right">
              <p>合肥</p>
              <sapn>周二</sapn>
            </div>
          </div>
          <div class="row">
            <div class="col-100 info-top-degrees">
              <p>19&deg;</p>
            </div>
          </div>
          <div class="row info-top-weather">
            <div class="col-50 info-top-left">
              <span>晴天</span>
            </div>
            <div class="col-50 info-top-right">
              <span>微风</span>
            </div>
          </div>
        </div>
      <div class="info-bottom">

      </div>
    </div>
</template>

<script>
    export default {
        mounted() {
            var ids=this.$router.params.id;
            var weather=JSON.parse(localStorage.setItem("WeatherData"));
            for(var i=0;i<weather.length;i++){
              if(i==ids){
                this.currentWeather=weather[i];
                break;
              }
            }
        },
        data() {
            return {
                currentWeather:{},
            }
        },
        methods: {
            demo() {
                console.log('demo fun')
            }
        }
    }
</script>

<style scoped>
  *{
    margin: 0;
    padding: 0;
  }
  .info{
    width: 100%;
    height: 100%;
  }
  .info-top{
    height: 100%;
    width: 100%;
    background: url("../../static/img/info_background.png") no-repeat center center;
    background-size: cover;
  }
  .info-top-city{
    padding:20% 10% ;
    padding-bottom: 0;
    color: #fff;
  }
  .info-top-left{
    text-align: right;
  }
  .info-top-right{
    text-align: left;
  }
  .info-top-degrees{
    color: #fff;
    font-size: 80px;
    text-align: center;
    margin-top: 40px;
  }
  .info-top-weather{
    color: #fff;
    margin-top: 50px;
  }

</style>

<template>
    <div>
        <a href="https://www.facebook.com/" target="_blank"><i class="fa fa-facebook" aria-hidden="true"></i><p style="display:none">Facebook</p></a>
        <a href="https://www.twitter.com/" target="_blank"><i class="fa fa-twitter" aria-hidden="true"></i><p style="display:none">Twitter</p></a>
        <a href="https://www.instagram.com/" target="_blank"><i class="fa fa-instagram" aria-hidden="true"></i><p style="display:none">Instagram</p></a>
         
    </div>
    
</template>
<script>
    define(["Vue", "vuex"], function(Vue, Vuex) {
        Vue.use(Lightbox);
        return Vue.component("weather-component", {
            template: template, // the variable template will be injected,
            computed: {
                
                weather() {
                    var openWeatherAPIKey = "c225dc6aeb2d6a1b39e8a463cedb62bd";
                    var openWeatherURL = "https://api.openweathermap.org/data/2.5/weather"+ "?id=6167865&APPID=" + openWeatherAPIKey + "&units=metric";
                    
                    var all_weather = {};
                    var vm = this;
                    axios.post(openWeatherURL).then(response => {
                     (response);
                      if(response && response.data && response.data.weather){
                        
                        var weather = response.data.weather[0];
                        weather.image_url = "http://openweathermap.org/img/w/"+weather.icon+".png"
                        vm.$set(all_weather, 'dets', weather)
                        vm.$set(all_weather, 'main', response.data.main);
                        vm.weatherDets = all_weather;
                      }
                    }).catch(error => {
                      console.log("Data load error: " + error.message);
                      (error);
                       return all_weather;
                    });
                }
            }
        });
    });
</script>
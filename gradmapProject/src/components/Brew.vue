<template>
    <div class="container">
        <div class="row">
            <div class="col-12">
                <h1 class="text-center text-info">Karadeniz Teknik Üniversitesi Harita Mühendisliği Mezun Öğrencilerin İş Haritası</h1>
            </div>
            <!-- /.col-121 -->
        </div>
        <!-- /.row -->
        <div class="row">
            <div class="col-6">
               <BrewList 
                  @mouse-over-brew="mouseOverBrew"
                  @mouse-left-brew="mouseLeftBrew"
                  :brews="brews"/>
               
            </div>
            <!-- /.col-6 -->
            <div class="col-6">
                <!-- insert map-->
              <BrewMap :brews="brews" />
            </div>
            <!-- /.col-6 -->
        </div>
        <!-- /.row -->


    </div>


</template>
<script>
  
  import axios from 'axios';
  import BrewList from './BrewList.vue';
  import BrewMap from './BrewMap.vue';

  export default {
    name: 'Brew',
    components:{BrewList,BrewMap},
    data: function () {
      return {
        brews: [],
        normalIcon: [15,15],
        largeIcon:[61,61]
      }
    },
    
    mounted: function(){
      axios.get('data.json')
        .then((r)=>{
          this.brews=r.data
            .map(r=>{
              r.iconSize=this.normalIcon;
              return r;
            })
        })
    },
     methods: {
            mouseOverBrew: function(index) {
                this.brews[index].iconSize=this.largeIcon;
            },
            mouseLeftBrew: function (index) {
                this.brews[index].iconSize=this.normalIcon;
            }
        }

  }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="scss" scoped>
</style>

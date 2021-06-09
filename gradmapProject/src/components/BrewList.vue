<template>
    
     <div class="card " >
                  <ul class="list-group list-group-flush brew-list">
                          <li 
                           @mouseover="mouseOver(index)"
                           @mouseleave="mouseLeave(index)"
                           v-bind:key="index"
                          class="list-group-item" v-for="(brew,index) in brews" 
                          >
                            {{brew.name}}
                            </li>
                    
                  </ul>
                </div>
</template>

<script>
    export default {
        name: "BrewList",
        props: {
            brews:Array
        },
         methods: {
            mouseOver: function (index) {
                this.$emit('mouse-over-brew', index);
            },
            mouseLeave: function (index) {
                this.$emit('mouse-left-brew', index);
            }
        }
            
    }
    </script>
<style lang="scss" scoped>
    .brew-list {
        overflow-y: scroll;
        height: 95vh;
        li {
            &:hover {
                background-color: darkgrey;
            }
        }
    }
</style>
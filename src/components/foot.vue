<template>
    <div class="hello">
      <nav class="bar bar-tab">
        <a class="tab-item external active" href="#">
          <span class="icon icon-home"></span>
          <span class="tab-label">文案</span>
        </a>
        <a class="tab-item external" href="#">
          <span class="icon icon-me"></span>
          <span class="tab-label">文案</span>
          <span class="badge">2</span>
        </a>
        <a class="tab-item external" href="#">
          <span class="icon icon-star"></span>
          <span class="tab-label">文案</span>
        </a>
        <a class="tab-item external" href="#">
          <span class="icon icon-cart"></span>
          <span class="tab-label">文案</span>
        </a>
        <a class="tab-item external" href="#">
          <span class="icon icon-settings"></span>
          <span class="tab-label">文案</span>
        </a>
      </nav>
    </div>
</template>

<script>
    export default {
        mounted() {
            this.demo()
        },
        data() {
            return {
                msg: 'dewdede'
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
  /*.bar-tab{*/
    /*!*display: none;*!*/
  /*}*/
</style>

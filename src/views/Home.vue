<template>
  <div class="home">
    <HelloWorld msg="tabs标签选择，取消demo"/>
    <select-tabs></select-tabs>
    
  </div>
</template>

<script>
// @ is an alias to /src
import HelloWorld from '@/components/HelloWorld.vue'
import selectTabs from './select-tabs.vue'
export default {
  name: 'home',
  components: {
    HelloWorld,
    selectTabs
  }
}
</script>

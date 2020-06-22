<template>
  <div id="app">
    <button @click="increment">
      Count is: {{ state.count }}, double is: {{ double }}
    </button>
    <div id="con">内容</div>
  </div>
</template>

<script>
import { reactive, computed } from 'vue'
import { watchEffect, watch, ref } from 'vue'

export default {
  setup() {
    // reactive类似于vue2的观察者observer
    const state = reactive({
      count: 0,
      num: 0,
    })
    // 用ref创建普通可变变量
    const exampel = ref(0)

    const double = computed(() => state.count * 2)
    // 方法，相当于vue2中的methods里的方法
    function increment() {
      state.count++, state.num++, exampel.value++
    }
    // 副作用
    watchEffect(() => {
      document.getElementById('con').innerHTML = `double is ${double.value}`
      console.log('exa', exampel.value)
    })
    // 与vue2中watch类似
    watch(
      () => state.num,
      (val, oldval) => {
        console.log(val, oldval)
      }
    )

    return {
      state,
      increment,
      double,
      watch,
      exampel,
    }
  },
}
</script>

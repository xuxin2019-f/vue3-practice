<template>
  <div>
    选择类型：
    <select v-model="state.type">
      <option value disabled>请选择/单选/多选</option>
      <option value="单选">单选</option>
      <option value="多选">多选</option>
    </select>
    请输入选择个数：
    <input type="text" placeholder="请输入选择个数" v-model="state.num" />
    <div class="radio">
      <p>单选框</p>
      <div class="radios" v-for="item in state.radios" :key="item.text">
        <input type="radio" name="radio" :value="item" v-model="state.radiopick" />
        <label for="item">{{item.text}}</label>
        <input type="text" :value="item.value" />
      </div>
    </div>
    <div class="checkbox">
      <p>多选框</p>
      <div class="checks">
        <!-- 多选框有不同的状态，可能不能用v-for？ -->
        <input
          type="checkbox"
          name="check"
          :value="state.checks[0]"
          class="checks-item"
          v-model="state.toggle[0]"
        />
        <label for="item">{{state.checks[0].text}}</label>
        <input type="text" :value="state.checks[0].value" />
        <input
          type="checkbox"
          name="check"
          :value="state.checks[1]"
          class="checks-item"
          v-model="state.toggle[1]"
        />
        <label for="item">{{state.checks[1].text}}</label>
        <input type="text" :value="state.checks[1].value" />
        <input
          type="checkbox"
          name="check"
          :value="state.checks[2]"
          class="checks-item"
          v-model="state.toggle[2]"
        />
        <label for="item">{{state.checks[2].text}}</label>
        <input type="text" :value="state.checks[2].value" />
      </div>
    </div>
    <button @click="submit">提交</button>
  </div>
</template>

<script>
import { reactive } from 'vue'
export default {
  setup() {
    const state = reactive({
      type: '',
      num: '',
      radios: [
        { text: 'A', value: '单选A' },
        { text: 'B', value: '单选B' },
        { text: 'C', value: '单选C' }
      ],
      radiopick: {},
      checks: [
        { text: 'A', value: '多选A' },
        { text: 'B', value: '多选B' },
        { text: 'C', value: '多选C' }
      ],
      toggle: [],
      options: [],
      anwser: []
    })
    function submit() {
      const checksitem = document.getElementsByClassName('checks-item')
      console.log(state.checksitem)
      if (state.type === '单选') {
        state.options = state.radiopick
        console.log(state.options)
        state.anwser.push(state.radiopick.value)
      } else {
        console.log(state.toggle)
        for (let i = 0; i < checksitem.length; i++) {
          if (state.toggle[i] === true) {
            console.log(checksitem[i].value)
            state.options.push(state.checks[i])
            state.anwser.push(state.checks[i].value)
          }
        }
      }
      console.log(`{
          type:${state.type},
          num:${state.num},
          options:${JSON.stringify(state.options)},
          anwser:${state.anwser}
         }`)
    }
    return {
      state,
      submit
    }
  }
}
</script>

<style>
</style>
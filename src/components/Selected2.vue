<template>
  <div>
    选择类型：
    <select v-model="type">
      <option value disabled>请选择/单选/多选</option>
      <option value="单选">单选</option>
      <option value="多选">多选</option>
    </select>
    请输入选择个数：
    <input type="text" placeholder="请输入选择个数" v-model="num" />
    <div class="radio">
      <p>单选框</p>
      <div class="radios" v-for="item in radios" :key="item.text">
        <input type="radio" name="radio" :value="item" v-model="radiopick" />
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
          :value="checks[0]"
          class="checks-item"
          v-model="toggle[0]"
        />
        <label for="item">{{checks[0].text}}</label>
        <input type="text" :value="checks[0].value" />
        <input
          type="checkbox"
          name="check"
          :value="checks[1]"
          class="checks-item"
          v-model="toggle[1]"
        />
        <label for="item">{{checks[1].text}}</label>
        <input type="text" :value="checks[1].value" />
        <input
          type="checkbox"
          name="check"
          :value="checks[2]"
          class="checks-item"
          v-model="toggle[2]"
        />
        <label for="item">{{checks[2].text}}</label>
        <input type="text" :value="checks[2].value" />
      </div>
    </div>
    <button @click="submit">提交</button>
  </div>
</template>

<script>
export default {
  data() {
    return {
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
    }
  },
  mounted() {
    this.checksitem = document.getElementsByClassName('checks-item')
    console.log(this.checksitem)
    this.submit()
  },
  methods: {
    submit() {
      // console.log('type', this.radiopick)
      if (this.type === '单选') {
        this.options = this.radiopick
        console.log(this.options)
        this.anwser.push(this.radiopick.value)
      } else {
        console.log(this.toggle)
        for (let i = 0; i < this.checksitem.length; i++) {
          if (this.toggle[i] === true) {
            console.log(this.checksitem[i].value)
            this.options.push(this.checks[i])
            this.anwser.push(this.checks[i].value)
          }
        }
      }
      console.log(`{
          type:${this.type},
          num:${this.num},
          options:${JSON.stringify(this.options)},
          anwser:${this.anwser}
         }`)
    }
  }
}
</script>

<style>
</style>
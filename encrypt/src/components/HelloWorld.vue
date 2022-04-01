<template>
  <div id="main" :style="{ height: this.height }">
    <div id="body">
      <div class="content">
        待加密/解密内容：<br />
        <el-input
          type="textarea"
          v-model="input"
          placeholder="请输入内容"
          style="width: 80%"
          :autosize="{ minRows: 4, maxRows: 8 }"
        ></el-input>
      </div>
      <div class="content" id="mid">
        <el-switch
          v-model="model"
          active-text="加密"
          inactive-text="解密"
          inactive-color="#13ce66"
        >
        </el-switch> <br /> <br />
        <el-input-number v-model="code" @change="handleChange" :min="1" :max="10" label="描述文字"></el-input-number>
      </div>
      <div class="content">
        输出内容：<br />
        <el-input
          type="textarea"
          v-model="output"
          placeholder="请输入内容"
          style="width: 80%"
          :autosize="{ minRows: 4, maxRows: 8 }"
        ></el-input>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  data () {
    return {
      input: `Yfqp nx hmjfu
Bmjwj ymjwj nx f xmjqq ymjwj nx f bfd
Xmtb rj ymj htij`,
      output: '',
      code: 1,
      model: true,
      height: window.innerHeight + 'px'
    }
  },
  mounted () {
    this.decrypt()
  },
  watch: {
    input () {
      this.decrypt()
    },
    code () {
      this.decrypt()
    },
    model () {
      this.decrypt()
    }
  },
  methods: {
    decrypt () {
      this.output = ''
      for (let i of this.input) {
        if (i === '\n') {
          this.output += '\n'
        } else if (i === ' ') {
          this.output += i
        } else {
          let temp
          if (this.model === true) temp = i.charCodeAt() + this.code
          else if (this.model === false) temp = i.charCodeAt() - this.code
          if (i.charCodeAt() >= 'a'.charCodeAt() && i.charCodeAt() <= 'z'.charCodeAt()) {
            if (temp < 'a'.charCodeAt()) temp += 26
            else if (temp > 'z'.charCodeAt()) temp -= 26
          } else if (i.charCodeAt() >= 'A'.charCodeAt() && i.charCodeAt() <= 'Z'.charCodeAt()) {
            if (temp < 'A'.charCodeAt()) temp += 26
            else if (temp > 'Z'.charCodeAt()) temp -= 26
          }
          this.output += String.fromCharCode(temp)
        }
      }
      console.log(this.output)
    }
  }
}
</script>

<style scoped>
#main {
  width: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
}

#body {
  width: 60%;
  height: 50%;
  display: flex;
  justify-content: center;
}

.content {
  width: 80%;
}
</style>

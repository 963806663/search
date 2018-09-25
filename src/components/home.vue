<template>
  <div class="content">
    <el-row>
      <el-col :span="12" :offset="6">
        <div class="grid-content bg-purple-dark" style="margin-top: 100px">
          <el-input @focus="show" v-model="text" placeholder="请输入内容"></el-input>
        </div>
      </el-col>
    </el-row>
    <lookup v-if="showLookup" v-on:child-say="listen"></lookup>
  </div>
</template>

<script>
  import lookup from './public/lookup'
export default {
    components:{
      lookup
    },
  data () {
    return {
      showLookup:false,
      text:''
    }
  },
  methods:{
    show(){
      if(!this.text){
        this.showLookup = true
      }
    },
    listen(data,text){
      this.showLookup = data;
      if(text){
        this.text = text
      }
    }
  }
}
</script>

<style scoped>
  .content{
    width: 100%;
    position: relative;
  }
  .bg-purple-dark {
    background: #99a9bf;
  }
  .grid-content {
    border-radius: 4px;
    min-height: 36px;
  }
</style>

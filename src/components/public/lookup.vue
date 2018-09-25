<template>
  <div class="content">
    <el-row>
      <el-col :span=8 offset=2>
        <div class="grid-content bg-purple-dark box1">
          <el-tree :data="data" :props="defaultProps" @node-click="handleNodeClick"></el-tree>
        </div>
      </el-col>
      <el-col :span=2>
        <div class="grid-content bg-purple-dark box2">
          <p style="font-size: 16px">添加</p>
          <p @click="showList">></p>
        </div>
      </el-col>
      <el-col :span=10>
        <div class="grid-content bg-purple-dark box3">
          <p>已选人员</p>
          <ul>
            <li v-for="(item,index) in list">
              <span>{{index+1}}.{{item.name}}</span>
              <span>{{item.post}}</span>
            </li>
          </ul>
        </div>
      </el-col>
    </el-row>
    <el-row style="position: absolute;bottom: 30px;width: 100%">
      <el-col :span=3 offset=6>
        <div class="grid-content bg-purple-dark box1">
          <el-button type="primary" @click="sure">确定</el-button>
        </div>
      </el-col>
      <el-col :span=3 offset=6>
        <div class="grid-content bg-purple-dark box2">
          <el-button type="primary" @click="cancel">取消</el-button>
        </div>
      </el-col>
    </el-row>
  </div>
</template>

<script>
  export default {
    data() {
      return {
        data:[],

        defaultProps: {
          children: 'children',
          label: 'name'
        },

        selected:'',

        list:[]
      };
    },
    methods: {
      handleNodeClick(data) {
        this.selected = data;
      },

      showList(){
        if(!this.selected){
          return;
        }
        //判断是否是最后一层
        if(this.selected.children){
          let arr  = this.selected.children;
          for(let i = 0; i< arr.length;i++){
            let item = arr[i];
            if(item.children){
              for(let j = 0; j <item.children.length;j++){
                this.list.push(item.children[j]);
              }
            } else{
              this.list.push(item);
            }
          }
        } else{
          this.list.push(this.selected);
        }
      },

      sure(){
        let text = '';
        if(this.list.length){
          text = JSON.stringify(this.list);
        }
        this.$emit('child-say',false,text);

      },
      cancel(){
        this.$emit('child-say',false);
      }
    },
    mounted(){
      let self = this;
      this.axios({
        methods:'get',
        url:"../../static/persons.json"
      }).then(function (res) {
        self.data = res.data;
      })
    }
  };
</script>

<style scoped>
  .content{
    padding-top: 30px;
    position: absolute;
    width: 80%;
    top: 100px;
    background: #ffffff;
    min-height: 500px;
    border: 1px solid;
    margin-left: 50%;
    transform: translateX(-50%);
  }
  .el-row{

  }
  .box1{

  }
  .box2 p{
    user-select: none;
    font-size: 50px;
    cursor:pointer;
    text-align: center;
  }
  .box3{
    text-align: center;
  }
</style>

<template>
  <div class="hello">
      <div class="content">
          <div class="top">
             <div v-if="go == 1"><img class="img_one" v-for="(item,index) in arrMax" :key="index" :src="item" alt=""></div>
            <div v-else><img class="img_one" v-for="(item,index) in arrThree" :key="index"  :src="item.path" alt=""></div>
          </div>
          <div class="left">
            <div class="left_son">
               <img v-for="(item,index) in arrLeft" :key="index" :src="item.path" alt="">
            </div>
          </div>
          <div class="right">
            <div class="right_son">
               <img v-for="(item,index) in arrRight" :key="index" :src="item.path" alt="">
            </div>
          </div>
          <div class="bottom">
            <img v-for="(item,index) in arrBottom"  @dragstart="dragfunc" :key="index" @mousemove="movefunc(index)" @click="clickSele(item,index)" @mouseup="upfunc(index)" @mousedown="downfunc(index)" :class="item.isSelect == 1? tops :''"  :src="item.path" alt="">
          </div>
          <div class="center">
              <button v-if="goTime==1" @click="goTimes()" class="goTime">开始</button>
              <div v-if="center == 1" class="center_botton">
                      <button @click="getbranch(1)" class="goTime_one">1 分</button>
                      <button @click="getbranch(2)" class="goTime_one">2 分</button>
                      <button @click="getbranch(3)"  class="goTime_one">3 分</button>
                      <button @click="getbranch(0)"  class="goTime_one">不叫</button>
              </div>
              <div v-if='djsClass == 1' class="djs posiCenter">{{djsNum}}</div>
              <div v-if='djsClass == 2' class="djs posiList">{{djsNum}}</div>
              <div v-if='djsClass == 3' class="djs posiRight">{{djsNum}}</div>
          </div>
      </div>
  </div>
</template>
<script>
 /* eslint-disable */
 let _ = require('lodash')
export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },
  data: function() {
      return {
        djsClass:0,//显示倒计时
        djsNum:30,//倒计时数字
        timer:'',
        signIndex:'',
        up:0,//判断鼠标有没有摁下
        goTime:1,
        center:0,
        tops:'tops',
        go:1,
        arrMax:[],//总牌数
        arrLeft:[],
        arrRight:[],
        arrBottom:[],
        arrThree:[],//最后三张
        arrMaxObj:[
          {index:0,path:require('../assets/img/1.jpg'),isSelect:0,name:'3'},
          {index:1,path:require('../assets/img/2.jpg'),isSelect:0,name:'3'},
          {index:2,path:require('../assets/img/3.jpg'),isSelect:0,name:'3'},
          {index:3,path:require('../assets/img/4.jpg'),isSelect:0,name:'3'},
          {index:4,path:require('../assets/img/5.jpg'),isSelect:0,name:'4'},
          {index:5,path:require('../assets/img/6.jpg'),isSelect:0,name:'4'},
          {index:6,path:require('../assets/img/7.jpg'),isSelect:0,name:'4'},
          {index:7,path:require('../assets/img/8.jpg'),isSelect:0,name:'4'},
          {index:8,path:require('../assets/img/9.jpg'),isSelect:0,name:'5'},
          {index:9,path:require('../assets/img/10.jpg'),isSelect:0,name:'5'},
          {index:10,path:require('../assets/img/11.jpg'),isSelect:0,name:'5'},
          {index:11,path:require('../assets/img/12.jpg'),isSelect:0,name:'5'},
          {index:12,path:require('../assets/img/13.jpg'),isSelect:0,name:'6'},
          {index:13,path:require('../assets/img/14.jpg'),isSelect:0,name:'6'},
          {index:14,path:require('../assets/img/15.jpg'),isSelect:0,name:'6'},
          {index:15,path:require('../assets/img/16.jpg'),isSelect:0,name:'6'},
          {index:16,path:require('../assets/img/17.jpg'),isSelect:0,name:'7'},
          {index:17,path:require('../assets/img/18.jpg'),isSelect:0,name:'7'},
          {index:18,path:require('../assets/img/19.jpg'),isSelect:0,name:'7'},
          {index:19,path:require('../assets/img/20.jpg'),isSelect:0,name:'7'},
          {index:20,path:require('../assets/img/21.jpg'),isSelect:0,name:'8'},
          {index:21,path:require('../assets/img/22.jpg'),isSelect:0,name:'8'},
          {index:22,path:require('../assets/img/23.jpg'),isSelect:0,name:'8'},
          {index:23,path:require('../assets/img/24.jpg'),isSelect:0,name:'8'},
          {index:24,path:require('../assets/img/25.jpg'),isSelect:0,name:'9'},
          {index:25,path:require('../assets/img/26.jpg'),isSelect:0,name:'9'},
          {index:26,path:require('../assets/img/27.jpg'),isSelect:0,name:'9'},
          {index:27,path:require('../assets/img/28.jpg'),isSelect:0,name:'9'},
          {index:28,path:require('../assets/img/29.jpg'),isSelect:0,name:'10'},
          {index:29,path:require('../assets/img/30.jpg'),isSelect:0,name:'10'},
          {index:30,path:require('../assets/img/31.jpg'),isSelect:0,name:'10'},
          {index:31,path:require('../assets/img/32.jpg'),isSelect:0,name:'10'},
          {index:32,path:require('../assets/img/33.jpg'),isSelect:0,name:'11'},
          {index:33,path:require('../assets/img/34.jpg'),isSelect:0,name:'11'},
          {index:34,path:require('../assets/img/35.jpg'),isSelect:0,name:'11'},
          {index:35,path:require('../assets/img/36.jpg'),isSelect:0,name:'11'},
          {index:36,path:require('../assets/img/37.jpg'),isSelect:0,name:'12'},
          {index:37,path:require('../assets/img/38.jpg'),isSelect:0,name:'12'},
          {index:38,path:require('../assets/img/39.jpg'),isSelect:0,name:'12'},
          {index:39,path:require('../assets/img/40.jpg'),isSelect:0,name:'12'},
          {index:40,path:require('../assets/img/41.jpg'),isSelect:0,name:'13'},
          {index:41,path:require('../assets/img/42.jpg'),isSelect:0,name:'13'},
          {index:42,path:require('../assets/img/43.jpg'),isSelect:0,name:'13'},
          {index:43,path:require('../assets/img/44.jpg'),isSelect:0,name:'13'},
          {index:44,path:require('../assets/img/45.jpg'),isSelect:0,name:'14'},
          {index:45,path:require('../assets/img/46.jpg'),isSelect:0,name:'14'},
          {index:46,path:require('../assets/img/47.jpg'),isSelect:0,name:'14'},
          {index:47,path:require('../assets/img/48.jpg'),isSelect:0,name:'14'},
          {index:48,path:require('../assets/img/49.jpg'),isSelect:0,name:'15'},
          {index:49,path:require('../assets/img/50.jpg'),isSelect:0,name:'15'},
          {index:50,path:require('../assets/img/51.jpg'),isSelect:0,name:'15'},
          {index:51,path:require('../assets/img/52.jpg'),isSelect:0,name:'15'},
          {index:52,path:require('../assets/img/53.jpg'),isSelect:0,name:'16'},
          {index:53,path:require('../assets/img/54.jpg'),isSelect:0,name:'17'},
        ]
      };
  },
  methods: {
    // 获取总牌数54张
    getArrMax () {
      let that = this
          //  this.arrMax.push(require(`../assets/img/(${i}).jpg`))
      let i = 0
      let setImg = setInterval(function(){
        i++
        that.arrMax.push(require(`../assets/img/timg.jpg`))
        if(i>=54){
          clearInterval(setImg);
        }
      },50)
      console.log(this.arrMax)
    },
    // 开始按钮
    goTimes () {
      this.goTime = 0
      let that  = this
      this.share().then(function(arr){
        let i = 0
        let setImg = setInterval(function(){
          i++
          that.shareOne(i,arr)
          if(i>=53){
            clearInterval(setImg);
            that.sortBy()
            that.go = 0
            that.center = 1
          }
        },50)
      })
    },
    // 本家 喊分
    getbranch (i) {
      if(i == 3){
        this.arrBottom.push(...this.arrThree)
        this.arrBottom = _.sortBy(this.arrBottom, function(item) {
          return -item.index;
        });
        this.arrThree=[]
        this.center = 0
        this.djsClass = 1
        this.djsFunction()
      }
    },
    // 打论扑克顺序
    share () {
      let that  = this
      return new Promise(function(resolve, reject){
          let  arr = that.arrMaxObj
          let i = arr.length; 
          while (i) { 
              let j = Math.floor(Math.random() * i--); 
              [arr[j], arr[i]] = [arr[i], arr[j]]; 
          } 
        resolve(arr)
      })
    },
    // 分配扑克
    shareOne(i,arr){
       i = i-1
       if(i<50){
          if(i % 3 == 1){
          this.arrLeft.push(arr[i])
          }else if(i % 3 == 2){
              this.arrRight.push(arr[i])
          }else if(i % 3 == 0){
              this.arrBottom.push(arr[i])
          }
       }else{
           this.arrThree.push(arr[i])
       }
    },
    // 排序
   sortBy () {
     let that = this
    this.arrLeft = _.sortBy(this.arrLeft, function(item) {
      return -item.index;
    });
    this.arrRight = _.sortBy(this.arrRight, function(item) {
      return -item.index;
    });
      this.arrBottom = _.sortBy(this.arrBottom, function(item) {
      return -item.index;
    });
   },
  //  30秒倒计时
   djsFunction () {
     this.djsNum = 30
     let that = this
     let djs = setInterval(function(){
       that.djsNum--
       if(that.djsNum ==1 ){
         clearTimeout(djs)
       }
     },1000)
   },
  //  点击单张扑克
  clickSele (item,index) {
    this.arrBottom[index].isSelect = this.arrBottom[index].isSelect == 1 ? 0 : 1
  },
  // 鼠标摁下 抬起事件
  downfunc (index){
     this.up = 1
  },
  upfunc (index) {
    this.up = 0
  },
  movefunc (index){
    let that = this
    if(this.up == 1){
      if(index != this.signIndex){
         that.arrBottom[index].isSelect = that.arrBottom[index].isSelect == 1 ? 0 : 1
      }else{
        if (this.timer) {clearTimeout(this.timer)}
          this.timer = setTimeout(function(){
            console.log(1)
            that.arrBottom[index].isSelect = that.arrBottom[index].isSelect == 1 ? 0 : 1
          },300)
        }
    }
    this.signIndex = index
  },
  dragfunc (e){
    console.log(121231)
     e.preventDefault()
    return false
  }
  },
  mounted(){
    this.getArrMax()
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.hello{
  width: 100%;
  height:auto;
  overflow: hidden;
}
.content{
  width: 90%;
  height: 700px;
  margin:0 auto;
  background-image: url(../assets/123.jpg);
  background-size: 100% 100%;
  background-repeat: no-repeat;
  background-position: center;
  position: relative;
}
.top{
  width: 80%;
  height: 150px;
  border:1px solid red;
  position: absolute;
  top: 0px; 
  left:10%;
  text-align: center;
  overflow: hidden;
}
.img_one{
  width: 50px;
  height: 100px;
  margin-left: -35px;
}

.left_son>img{
    width: 50px;
    height: 100px;
    margin-left: 35px;
    margin-top: -80px;
    display: block;
    transform: rotate(90deg);
}
.right_son>img{
    width: 50px;
    height: 100px;
    margin-left: 35px;
   margin-top: -80px;
    display: block;
    transform: rotate(-90deg);
}
.right_son>img:nth-child(1){
  margin-top: 0px;
}
.left_son>img:nth-child(1){
  margin-top: 0px;
}
.bottom>img{
  width: 60px;
  height: 110px;
  margin-left: -35px;
  margin-top: 35px;
  position: relative;
}
.left{
  height: 80%;
  width: 10%;
  border:1px solid red;
  position: absolute;
  left: 0px; 
  top:10%;
}
.left_son{
  width: 100%;
  height: 80%;
  position: absolute;
  top:10%;
}
.right{
  height: 80%;
  width: 10%;
  border:1px solid red;
  position: absolute;
  right: 0px; 
  top:10%;
}
.right_son{
  width: 100%;
  height: 80%;
  position: absolute;
  top:10%;
}
.bottom{
  width: 80%;
  height: 150px;
  border:1px solid red;
  position: absolute;
  bottom: 0px; 
  left:10%;
}
.center{
  width: 80%;
  height: 400px;
  position: absolute;
  top: 150px;
  left: 10%;
  bordeR:4px solid black;
}
.goTime{
  width: 60px;
  height: 25px;
  background: #fff;
  border-radius: 3px;
  font-size: 13px;
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%,-50%);
}
.center_botton{
  width: 100%;
  height: 30px;
  position: absolute;
  bottom: 5px;
  text-align: center;
}
.goTime_one{
   width: 60px;
  height: 25px;
  background: #fff;
  border-radius: 3px;
  font-size: 13px;
  margin: 0 5px;

}
.djs{
  width: 40px;
  height: 40px;
  border-radius: 50%;
  color: #fff;
  background-color: #23aec4;
  font-size: 14px;
  font-weight: 600;
  text-align: center;
  line-height: 40px;
}
.posiCenter{
  position: absolute;
  bottom:2%;
  left: 50%;
  transform: translate(-50%,-50%); 
}
.posiList{
  position: absolute;
  top:50%;
  left: 2%;
  transform: translate(-50%,-50%); 
}
.posiRight{
  position: absolute;
  top:50%;
  right: 2%;
  transform: translate(-50%,-50%); 
}
.tops{
  top:-15px;
}

</style>


<template>
    <div>
      <section class="header">
        <div class="logo">
          <img src="../assets/img/logo/665984.png"  alt="NIMO" height="36" />
        </div>
        <div class="nav">
          <ul>
            <li><a class="selected" href="">首页</a></li>
            <li><a href="">网络信息查询</a></li>
            <li><a href="">个人信息变更</a></li>
            <li><a href="">故障处理询</a></li>
            <li><a href="">投诉与建议</a></li>
          </ul>
        </div>
        <div class="user">
          <a href="">使用jAccount登录</a>
        </div>
      </section>
      <section class="home">
        <div class="logoBar row">
          <img src="../assets/img/logo/SJTU-NIMO.svg"  alt="NIMO" height="70" />
        </div>
        <div class="row">
          <div class="news">
            <div class="title">
              <h3>新闻公告 </h3>
              <a href="" class="more">MORE</a>
            </div>
            <ul>
              <li v-for="item in newsList" :key="item.index" class="newsItem">
                <a :href="item.link">
                  <div class="title_text">{{item.title}}</div>
                  <div class="time">{{item.time}}</div>
                </a>
              </li>
            </ul>
            <div class="now">当前值班状态： <strong>休息中</strong></div>

          </div>
          <div class="contactUs">
            <div class="title">
              <h3>联系我们</h3>
            </div>
            <h4>闵行校区网管部</h4>
            <p>
              <span >电  话：</span>
              <span >54745261</span>
            </p>
            <p>
              <span >地  址：</span>
              <span >蓁蓁楼3楼活动室</span>
            </p>            
            <p>
              <span >值班时间：</span>
              <span >工作日：16:00-20:00</span>
              <span class="worktime">周 三：14:00-20:00</span>
              <span class="worktime">休息日：14:00-18:00</span>
            </p>
            <h4 class="titleX">徐汇校区网管部</h4>
            <p>
              <span >电  话：</span>
              <span >62934784 转 802</span>
            </p>
            <p>
              <span >地  址：</span>
              <span >徐汇学生服务中心</span>
            </p>            
            <p>
              <span >值班时间：</span>
              <span >工作日：18:00-20:00</span>
            </p>
          </div>
        </div>

        <div class="btns row">
          <ul>
            <li class="btn">
              <a href="">
                <img src="../assets/img/icons/netapply.png"  alt="netapply" height="64" />
                <h3>开网教程</h3>
              </a>
            </li>
            <li class="btn">
              <a href="">
                <h3>了解我们</h3>
                <img class="down" src="../assets/img/icons/downward.png"  alt="netapply" height="64" />
              </a>
            </li>
            <li class="btn">
              <a href="">
                <img src="../assets/img/icons/joinus.png"  alt="joinUs" height="64" />
                <h3>加入我们</h3>
              </a>
            </li>
          </ul>
        </div>

        <div class="about">        
          <button @click="previous" class="left">
            &lt;
          </button>

          <!-- 动画摸不出来 呜呜 -->
          <div class="shell">
            <div class="images">
              <!-- <transition-group name="direction" > -->
                <li v-for="(pic,index) in picList" :key="pic">
                  <img 
                    v-show="index==currentIndex"
                    :src="pic"
                    alt="about_us_pic" 
                  />
                </li>
              <!-- :class="[{'active': index==currentIndex,'inactive':index!=currentIndex}]" -->
          <!-- </transition-group> -->
            </div>
              <ul class="lines">
                <li v-for="(pic,index) in picList" :key="pic"
                  @click="goto(index)"
                >
                  <button 
                    :class="[{'active': index==currentIndex,  'inactive':index!=currentIndex}]">
                  </button>
                </li>
              </ul>
          </div>

          <button @click="next" class="right">
            >
          </button>
        </div>

        <div class="end row">
          <p>oScope</p>
          <p>© 2017-2022 Powered by NIMOdev.</p>
        </div>

      </section>
        
    </div>
</template>

<script>
  // 引入图片
  import img1 from '../assets/img/aboutus/1.png';
  import img2 from '../assets/img/aboutus/2.png';
  import img3 from '../assets/img/aboutus/3.png';
  import img4 from '../assets/img/aboutus/4.png';
  import img5 from '../assets/img/aboutus/5.png';

  export default {
    data() {
      return {
        value: 0,
        newsList:[
          {
            title:'1月25日值班公告',
            time: '2022-01-25',
            link:'https://nimo.sjtu.edu.cn/kaleid/oscope/home/announcement/88',
          },
          {
            title:'2022寒假值班公告',
            time: '2022-01-16',
            link:'https://nimo.sjtu.edu.cn/kaleid/oscope/home/announcement/87',
          },
          {
            title:'元旦及考试周期间值班报修暂停通知',
            time: '2021-12-30',
            link:'https://nimo.sjtu.edu.cn/kaleid/oscope/home/announcement/86',
          },
          {
            title:'12月26日网管部值班报修暂停公告',
            time: '2021-12-24',
            link:'https://nimo.sjtu.edu.cn/kaleid/oscope/home/announcement/85',
          },
          {
            title:'中心组换届通知',
            time: '2021-10-07',
            link:'https://nimo.sjtu.edu.cn/kaleid/oscope/home/announcement/84',
          },
          {
            title:'国庆节期间网管部值班报修安排',
            time: '2021-09-30',
            link:'https://nimo.sjtu.edu.cn/kaleid/oscope/home/announcement/83',
          },
        ],
        picList:[
          img1,img2,img3,img4,img5,
        ],
        currentIndex: 0,
        timer: null,
        direction: 'slideLeft',
      }
    },
    
    mounted() {
      this.timer = setInterval(() => {
        this.next();
      }, 2500)
    },
    
    methods: {
      test() {
        console.log('this.currentIndex = ',this.currentIndex);
      },

      previous() {
        if(this.currentIndex<=0) {
          this.currentIndex = 4;
        } else {
          this.currentIndex -= 1;
        }
        clearInterval(this.timer);
        this.autoPlay();
        // this.direction = 'slideRight';
      },
      next() {
        if(this.currentIndex>=4) {
          this.currentIndex = 0;
        } else {
          this.currentIndex += 1;
        }
        clearInterval(this.timer);
        this.autoPlay();
        // this.direction = 'slideLeft';
      },
      goto(index) {
        this.currentIndex = index;
        clearInterval(this.timer);
        this.autoPlay();
      },

      autoPlay() {
        this.timer = setInterval(() => {
          this.next();
        }, 2500)
      }
    }
  }
</script>

<style scoped>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

* {
  margin: 0;
  padding: 0;
}
li {
  list-style: none;
}
a{
  text-decoration: none;
}

/* header */
.header{
  font-size: 16px;
  font-weight: 800;
  background-color: #3F2155;
  margin: 0;
  height: 55px;
}
.logo {
  float: left;
  height: 36px;
  margin-left: 20px;
  margin-top: 7px;
}
.nav {
  float: left;
  margin-left: 30px;
}

.nav ul li {
  float: left;
  margin: auto 0px;
}

.nav ul li a  {
  display:block;
  height: 54px;
  line-height: 48px;
  padding: 0 20px;
  color: #665884;
  border-top: 5px solid #3F2155;
}
.nav ul li a.selected {
  color: #ffffff;
  border-top: 5px solid #665884;

}
.nav ul li a:hover {
  border-top: 5px solid #665884;
  color: #ffffff;
}
.user {
  float: right;
  margin-right: 20px;
}
.user a {
  line-height: 55px;
  height: 55px;
  color: #cccccc;
}
/* header */

.row {
  width: 970px;
  display: inline-block;
  margin: auto;
}

.logoBar img {
  float: left;
  margin-left: 0;
  margin-top: 50px;
  margin-bottom: 70px;
}

/* ------ news section ----- */
.news {
  float: left;
  margin-left: 0;
  width: 700px;
  color:#ffffff;
}

.title {
  border-bottom: 1px solid #ffffff;
  text-align: left;
}
.title h3 {
  display: inline;
  font-size: 30px;
  line-height: 50px;
  color:#ffffff;
  font-weight: 600;
}

.news a.more {
  font-size: 12px;
  color:#ffffff
}

.news ul {
    border-bottom: 1px solid #ffffff;
}
li.newsItem a {
    display:block;
    line-height: 45px;
    height: 45px;
    font-weight: 600;
    font-size: 16px;
    background-color: transparent;
    color:#ffffff;
}
li.newsItem a:hover {
    background-color: rgba(0,0,0,0.4);
}

li.newsItem a .title_text {
    float: left;
    padding-left: 5px;
}
li.newsItem a .time {
    float: right;
    padding-right: 50px;
}
.news .now {
  padding-top: 10px;
}
/* ------ news section ----- */

/* ------ contact us section ----- */
.contactUs {
  float: right;
  width: 240px;
  text-align: left;
  color:#ffffff;
}

.contactUs h4 {
  font-size: 18px;
  margin: 10px 0;
}

.contactUs p {
  font-size: 14px;
  /* line-height: 24px; */
  margin: 5px 0;
}
.contactUs .worktime {
  margin-left: 70px;
}

.contactUs .titleX {
  padding-top: 20px;
}

/* ------ contact us section ----- */

/* ------ buttons ----- */
.btns {
  margin-top: 40px;
  margin-bottom: 20px;
}
.btns .btn a {
  float: left;
  width: 33%;
  height: 160px;
  border-radius: 20px;
  color: #ffffff;
  background-color: transparent;
}
.btns .btn a:hover {
  background-color: rgba(0,0,0,0.2);
}
.btns .btn img {
  margin-top: 15px;
}
.btns .btn h3 {
  color: #ffffff;
  font-size: 24px;
  margin: 15px auto;
}

.btns .down {
  animation:mymove 3s infinite;
}

@keyframes mymove
{
  0%   {opacity: 0}
  50%  {opacity: 1}
  100%   {opacity: 0}
}

@-webkit-keyframes mymove /*Safari and Chrome*/
{
  0%   {opacity: 0}
  50%   {opacity: 1}
  100%   {opacity: 0}
}
/* ------ buttons ----- */

/* ------ about us----- */
.about {
  display: inline-block;
  width: 100%;
  background-color: rgba(51, 37, 94, 0.55);
}

.shell {
  position: relative;
  width: 650px;
  height: 720px;
  overflow: hidden;
  margin: 0 auto;
  display: inline-block;
  /* border: 10px #fff solid; */

}

/* .about .images {
  width: vw*5 ;
  height: 100%;
  display: flex;
  position: absolute;
  left: 0;
} */
.about img {
  height: 720px;
  width: auto;
  z-index:1;
  /* float: left; */
  
  /* max-width: 80vh; */
}

.about button {
  background-color: transparent;
  border: none;
  color: #fff;
  margin-top: 330px;
  width: 36px;
  height: 36px;
  cursor: pointer;
}
.about button:hover {
  color: #cccccc;
}

.about button.left {
  float: left;
  margin-left: 20px;
}

.about button.right {
  float: right;
  margin-right: 20px
}

/* .active {
  opacity: 1;
}
.inactive {
  opacity: 0.5;
} */

/* 摸不出来动画 呜呜 */
.slideRight-enter-active, .slightRight-leave-active {
  transition: all 1s;
}
.slightRight-enter, .slideRight-leave-to {
  opacity: 0;
  transform: translateX(100%);
}


.lines {
  width: 190px;
  height: 20px;
  position: absolute;
  left: 235px;
  z-index: 9;
  margin-top: -20px;
}
.lines li {
  float: left;
  width: 30px;
  height: 10px;
  margin: auto 3px;
  /* background-color: pink; */
  cursor: pointer;
}

.lines li button {
  float: left;
  width: 30px;
  height: 2px;
  margin-top: 2px;
  background-color: #ffffff;
}
.lines .active {
  opacity: 1;
}

.lines .inactive {
  opacity: 0.7;
}



/* ------ about us----- */

/* ------ end copyright----- */
.end {
  margin: 35px auto;
  font-size: 16px;
  font-weight: 500;
  color: rgb(204, 153, 255);
}
.end p {
  margin-bottom: 15px;
}

</style>
<template>
  <div class="home">
    <!-- 外层容器 -->
    <el-container>
      <!-- 头部 -->
      <el-header class="home_header">
        <div>
          <img style="width:50px; height:50px" src="./logo.png">
          <span>绝对玩家</span>
        </div>
      </el-header>
      
      <!-- 二级容器 -->
      <el-container>
        <!-- main -->
        <el-main class="home_main">
          <div style="width:600px">
            <!-- <el-carousel height="150px">
              <el-carousel-item v-for="item in 4" :key="item">
                <h3>{{ item }}</h3>
              </el-carousel-item>
            </el-carousel> -->
            <el-carousel height="300px">
              <el-carousel-item v-for="item in slide" :key="item.id">
                <img style="width:100%" src="./logo.png">
              </el-carousel-item>
            </el-carousel>
          </div>
          <div style="margin-top:20px;">
            <h4 class="banner">热点资讯</h4>
            <ul>
              <li v-for="item in newsList" :key="item.id" class="news_list">
                <span>
                  <a @click="getDetail(item.id)">{{item.title}}</a>
                </span>
                <em>{{item.date}}</em>     
              </li>
            </ul>
          </div>
          <div style="margin-top:20px;">
            <h4 class="banner">杂谈</h4>
            <ul>
              <li v-for="item in talkList" :key="item.id" class="news_list">
                <span>
                  <a @click="getDetail(item.id)">{{item.title}}</a>
                </span>
                <em>{{item.date}}</em>     
              </li>
            </ul>
          </div>
          <div style="margin-left:20%">
            <!-- 每页5条,共100条数据,所以是20页面 -->
            <el-pagination layout="prev, pager, next" :page-size="5" :total="100"></el-pagination>
          </div>
          <div style="margin-top:20px;">
            <h4 class="banner">游戏评测</h4>
            <ul>
              <li v-for="item in evaluationList" :key="item.id" class="news_list">
                <span>
                  <a @click="getDetail(item.id)">
                    {{item.title}}
                    <label style="color:#aaa;">{{item.about}}</label>
                  </a>          
                </span>
                <em style="color:#ff8700">{{item.rate}}</em>
              </li>
            </ul>
          </div>
          <div style="margin-top:20px;">
            <h4 class="banner">硬件频道</h4>
            <ul>
              <li v-for="item in hardwareList" :key="item.id" class="news_list">
                <span>
                  <a @click="getDetail(item.id)">
                    {{item.title}}
                  </a>          
                </span>
                <em style="color:#ff8700">最新 !</em>
              </li>
            </ul>
          </div>
        </el-main>

        <!-- aside -->
        <el-aside class="home_aside">
          <el-tabs v-model="activeName" @tab-click="handleClick">
            <!-- 空标签占位置 -->
            <el-tab-pane></el-tab-pane><el-tab-pane></el-tab-pane>
            <el-tab-pane label="单机排行" name="singleGamesRank">
              <ul style="list-style:none">
                <li v-for="(item, index) in singleGamesRankList" :key="item.id" class="news_list">
                  <span>
                    <i class="rank" v-bind:style="item.rankObject">{{item.rank}}</i>
                    <a @click="getDetail(item.id)">{{item.title}}</a>
                  </span>
                  <em style="color:#ff8700">{{item.rate}}</em>     
                </li>
              </ul>
            </el-tab-pane>
            <el-tab-pane label="单机更新" name="singleGamesUpdate">
              <ul style="list-style:none">
                <li v-for="(item, index) in singleGamesUpdateList" :key="item.id" class="news_list">
                  <span>
                    <i class="rank" v-bind:style="item.rankObject">{{item.rank}}</i>
                    <a @click="getDetail(item.id)">{{item.title}}</a>
                  </span>
                  <em style="color:#ff8700">{{item.rate}}</em>     
                </li>
              </ul>
            </el-tab-pane>
          </el-tabs>  



        </el-aside>
      </el-container>
    </el-container>
  </div>
</template>

<script>
export default {
  name: "home",
  data() {
    return {
      // 默认"单机排行标签"
      activeName: "singleGamesRank",
      // 轮播图
      slide: [
        {
          id: 1,
          url: "./logo.png"
        },
        {
          id: 2,
          url: "./logo.png"
        },
        {
          id: 3,
          url: "./logo.png"
        },
      ],
      // 新闻列表
      newsList: [
        {
          title: "震惊！99.99%的人都不知道的死法！",
          date: "2018-05-22",         
        },
        {
          title: "震惊！美国总统看到后都惊呆了！",
          date: "2018-05-22",         
        },
        {
          title: "震惊！一女子竟然光天化日之下做出这种事情！",
          date: "2018-05-22",         
        },
        {
          title: "震惊！父亲居然当着女儿的面做这种动作！",
          date: "2018-05-22",         
        },
        {
          title: "震惊！女子在医院对护士这样说话！",
          date: "2018-05-22",         
        },
        {
          title: "震惊！此老人竟然凭借此方法不老！",
          date: "2018-05-22",         
        },
        {
          title: "震惊！男人看了会沉默，女人看了会流泪！不转不是中国人！",
          date: "2018-05-22",         
        },
        {
          title: "李湘在大街上被人强行拖行",
          date: "2018-05-22",         
        },
        {
          title: "闹市中惊现悬挂于车外的裸尸",
          date: "2018-05-22",         
        },
        {
          title: "当红嫩模当街全裸任市民拍照",
          date: "2018-05-22",         
        },
        {
          title: "街头惊现两裸男暴雨中飙车",
          date: "2018-05-22",         
        },
        {
          title: "震惊！99.99%的人都不知道的死法！",
          date: "2018-05-22",         
        },
        {
          title: "震惊！美国总统看到后都惊呆了！",
          date: "2018-05-22",         
        },
      ],
      // 杂谈列表
      talkList: [
        {
          title: "[影视]时刻面临肾上腺素的爆发 16部末日题材美剧",
          date: "2018-05-10",         
        },
        {
          title: "看完《复联3》不过瘾 未来还有这14部超级英雄电影",
          date: "2018-05-10",         
        },
        {
          title: "[影视]剧情不输好莱坞大片 十部国产犯罪类型电影",
          date: "2018-05-10",         
        },
        {
          title: "[影视]《权力的游戏》变化最大的九人",
          date: "2018-05-10",         
        },
        {
          title: "上世纪60年代女性的老照片",
          date: "2018-05-10",         
        },
        {
          title: "女人的痛你不懂",
          date: "2018-05-10",         
        },
      ],
      // 游戏评测
      evaluationList: [
        {
          title: "刺客信条:起源",
          about: "第七部正统续作,是《刺客信条》系列历史上规模最大的一个",
          rate: "8.5",         
        },
        {
          title: "贪玩蓝月",
          about: "两周年狂欢,影帝服首发",
          rate: "9.0",         
        },
        {
          title: "绝地求生",
          about: "大吉大利今晚吃鸡",
          rate: "7.2",         
        },
      ],
      // 硬件频道
      hardwareList: [
        {
          title: "AMD新旗舰处理器2950X规格曝光 仍是16核32线程",     
        },
        {
          title: "15款游戏大作单双通道内存测试8G与16G有啥差别？",     
        },
        {
          title: "映泰再出挖主板 支持8路显卡板载16个6Pin供电接口",     
        },
      ],
      // 单机排行
      singleGamesRankList: [
        {
          title: "荒野行动",
          rate: "9.0",
          rank: 1,
          rankObject: {
            "color": "#fff",
            "background-color": "#f25324",
          },
        },
        {
          title: "看门狗2",
          rate: "9.0",
          rank: 2,
          rankObject: {
            "color": "#fff",
            "background-color": "#ff9908",
          },
        },
        {
          title: "模拟人生4",
          rate: "9.0",
          rank: 3,
          rankObject: {
            "color": "#fff",
            "background-color": "#fbd167",
          },
        },
        {
          title: "文明6",
          rate: "9.0",
          rank: 4,
        },
        {
          title: "掠杀原型2",
          rate: "9.0",
          rank: 5,
        },
        {
          title: "刺客信条:起源",
          rate: "9.0",
          rank: 6,
        },
        {
          title: "绝地求生",
          rate: "9.0",
          rank: 7,
        },
        {
          title: "DOTA2",
          rate: "9.0",
          rank: 8,
        },
        {
          title: "GTA5",
          rate: "9.0",
          rank: 9,
        },
        {
          title: "NBA2016",
          rate: "9.0",
          rank: 10,
        },
      ],
      // 单机更新
      singleGamesUpdateList: [
        {
          title: "红警",
          rate: "9.0",
          rank: 1,
          rankObject: {
            "color": "#fff",
            "background-color": "#f25324",
          },
        },
        {
          title: "魔兽",
          rate: "9.0",
          rank: 2,
          rankObject: {
            "color": "#fff",
            "background-color": "#ff9908",
          },
        },
        {
          title: "帝国",
          rate: "9.0",
          rank: 3,
          rankObject: {
            "color": "#fff",
            "background-color": "#fbd167",
          },
        },
        {
          title: "星际",
          rate: "9.0",
          rank: 4,
        },
        {
          title: "拳皇",
          rate: "9.0",
          rank: 5,
        },
        {
          title: "极品飞车",
          rate: "9.0",
          rank: 6,
        },
        {
          title: "火影忍者",
          rate: "9.0",
          rank: 7,
        },
        {
          title: "合金探头",
          rate: "9.0",
          rank: 8,
        },
        {
          title: "抢滩登陆",
          rate: "9.0",
          rank: 9,
        },
        {
          title: "cs",
          rate: "9.0",
          rank: 10,
        },
      ],
    };
  },
  methods: {
    getDetail: function (id) {
      window.open("http://wwww.baidu.com");
    },
    handleClick: function (tab, event) {
      console.log(tab, event);
    }
  }
};
</script>

<style scoped>
  .home_header {
    padding: 0;
  }
  .home_main {
    padding: 0;
    padding-right: 20px;
    width: 64%;
  }
  .home_aside {
    padding: 0;
    padding-left: 20px;
    width: 36% !important;
  }
  
  .banner {
    font-size: 22px;
    line-height: 22px;
    padding-left: 10px;
    color: #000;
    font-weight: 400;
    border-left: 5px solid #408ed6;
  }
  .news_list {
    font-family: "Simsun";
    color: #aaa;/* 用于li的原点,所以该节点下的其他地方需要重写color以覆盖 */
    height: 30px;
    /* font-size: 16px; */
    font-size: 16px;
  }
  /* .news_list a {
    width: 450px;
    display: block;
    white-space: nowrap;
    overflow: hidden;
    text-overflow: ellipsis;
  } */
  .news_list em {
    font-family: "arial";
    color: #aaa;
    float: right;
  }
  .rank {
    width: 20px;
    height: 20px;
    line-height: 20px;
    display: inline-block;
    font-style: normal;
    text-align: center;
    color: #777777;
    background-color: #eaeaea;
  }
  ul {
    padding-left: 15px;
  }
  a {
    text-decoration: none;
    cursor: pointer;
    color: #333;
  }
  a:hover {
    color: #f21000;
  }
</style>
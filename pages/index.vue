<template>
  <div class="container">
    <div class="home-header">
      <img src="/home-search-text.png" alt="img">
      <form action="">
        <input type="text" placeholder="搜索职位/公司">
        <button>搜索</button>
      </form>
    </div>
    <div class="home-categories">
      <dl v-for="item in categories" :key="item.name">
        <dt>
          <img :src="item.icon" alt="">
          <div>{{item.name}}</div>
        </dt>
        <dd>
          <!-- <a href="" class="tag" v-for='tag in item.tags' :key="tag">{{tag}}</a> -->
          <nuxt-link to="/list" class="tag" v-for='tag in item.tags' :key="tag">{{tag}}</nuxt-link>
        </dd>
      </dl>
    </div>
    <div class="home-footer">
      <p>违法和不良信息举报邮箱：jubao@kanzhun.com</p>
      <p>企业服务热线和举报投诉：400 065 5799</p>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      categories: [
        {
          "icon": "/technology.png",
          "name": "技术",
          "tags": ["Java", "PHP", "Web前端", "数据挖掘", "C++", "Python", "Android", "iOS"]
        },
        {
          "icon": "/product.png",
          "name": "产品",
          "tags": ["产品经理", "产品助理", "网页产品经理", "数据产品经理"]
        },
        {
          "icon": "/designer.png",
          "name": "设计",
          "tags": ["UI设计师", "平面设计师", "交互设计师", "设计总监"]
        },
        {
          "icon": "/market.png",
          "name": "市场",
          "tags": ["市场营销", "商务渠道", "品牌公关", "市场总监", "策划经理", "活动策划", "SEO", "SEM"]
        },
        {
          "icon": "/operate.png",
          "name": "运营",
          "tags": ["用户运营", "产品运营", "新媒体运营", "运营总监", "商家运营", "电商运营", "编辑", "客服运营"]
        },
        {
          "icon": "/senior.png",
          "name": "职能/高级管理",
          "tags": ["人力资源", "行政", "财务", "会计", "HRBP"]
        }
      ]
    }
  }
  // created:function() {
  //   const that = this
  //   fetch("http://localhost:3000/api/index.json").then(function(res) {
  //     // console.log(res);
  //     // console.log(res.json());
  //     return res.json()
  //   }).then(function(data) {
  //     that.categories = data
  //   })
  // } 
}
</script>

<style>
.home-header {
  background: url(/home-bg.png) no-repeat;
  background-size: 100% auto;
  text-align: center;
  padding-bottom: 1.5rem;
}
.home-header > img {
  width: 67%;
  margin: 2.3rem;
}
.home-header form {
  background-color: white;
  width: 90%;
  margin:0 auto;
  line-height: 2.2rem;
  border-radius: 2.2rem;
}
.home-header form input {
  width: 75%;
  border: 0;
  color: #aeaeae;
  font-size: 0.85rem;
  outline: none;
}
.home-header form button {
  font-size: 0.9rem;
  color: #5bd4c7;
  background-color: white;
  border: none;
  background: none;
}

.home-categories {
  padding: 0 1rem;
}
.home-categories dt {
  display: flex;
  align-items: center;
  color: #404855;
  margin: 0.5rem 0;
}
.home-categories dt img {
  height: 3rem;
  margin-right: 1rem;
}
.home-categories dd {
  margin: 0 -0.4rem;
  padding-bottom: 0.5rem;
  border-bottom: solid 1px #EEE;
}
.home-categories dd .tag {
  background-color: #f5f8f9;
  color: #7e8793;
  padding: 0.5rem 1rem;
  display: inline-block;
  border-radius: 2rem;
  text-decoration: none;
  margin: 0.2rem 0.4rem;
  font-size: 0.8rem;
}
.home-categories :last-child dd {
  border: none;
}

.home-footer {
  width: 70%;
  margin: 0 auto;
  font-size: 0.7rem;
}
.home-footer p {
  margin: 0.2rem 0;
}
</style>
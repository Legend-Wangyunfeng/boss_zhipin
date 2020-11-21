<template>
  <div class="container" id="app">
    <div class="list-header flex">
      
      <form action="" class="flex">
        <nuxt-link to="/">
          <img src="/icon-home.png" alt="">
        </nuxt-link>
        
        <div class="inner flex">
          <input type="text" placeholder="Java">
          <span>&times;</span>
        </div>
        <button>搜索</button>
      </form>
    </div>
    <div class="filter flex">
      <dl v-for="(item, index1) in filter" @click="changeCategories(index1)" :class="{active: index1 === index_categories}" :key="item.categories">
        <dt>{{item.categories}}</dt>
        <dd>
          <ul>
            <li :class="{active: index_options[index1] === index2}" v-for="(option, index2) in item.options" @click="changeOptions(index1,index2)" :key="option.id">{{option.text}}</li>
          </ul>
        </dd>
      </dl>

    </div>
    <ul class="job-list">
      <li v-for="item in company" :key="item.company">
        <nuxt-link to="/detail" class="job-item flex">
          <img :src="item.image" alt="">
          <div class="text">
            <div class="title flex">{{item.title}}<span class="salary">{{item.salary}}</span></div>
            
            <div class="company">{{item.company}}</div>
            <div class="props">
              <span v-for="i in item.tags" :key="i">{{i}}</span>
          </div>
          </div>
        </nuxt-link>
      </li>

    </ul>
  </div>
</template>

<script>
export default {
    data() {
      return {
        filter: [
          {
            "categories": "经验",
            "options": [
              {"text": "不限", "id": null},
              {"text": "在校生", "id": 1},
              {"text": "应届生", "id": 2},
              {"text": "1年以内", "id": 3},
              {"text": "3-5年", "id": 4},
              {"text": "5-10年", "id": 5}
            ]
          },
          {
            "categories": "学历",
            "options": [
              {"text": "不限", "id": null},
              {"text": "初中及以下", "id": 1},
              {"text": "中专/中技", "id": 2},
              {"text": "高中", "id": 3},
              {"text": "大专", "id": 4},
              {"text": "本科", "id": 5}
            ]
          },
          {
            "categories": "薪资",
            "options": [
              {"text": "不限", "id": null},
              {"text": "3K以下", "id": 1},
              {"text": "3-5K", "id": 2},
              {"text": "5-10K", "id": 3},
              {"text": "10-15K", "id": 4},
              {"text": "15-20K", "id": 5}
            ]
          },
          {
            "categories": "规模",
            "options": [
              {"text": "不限", "id": null},
              {"text": "0-20人", "id": 1},
              {"text": "20-90人", "id": 2},
              {"text": "100-499人", "id": 3},
              {"text": "500-999人", "id": 4},
              {"text": "1000-9999人", "id": 5}
            ]
          },
          {
            "categories": "融资",
            "options": [
              {"text": "不限", "id": null},
              {"text": "未融资", "id": 1},
              {"text": "天使轮", "id": 2},
              {"text": "A轮", "id": 3},
              {"text": "B轮", "id": 4},
              {"text": "C轮", "id": 5}
            ]
          }
        ],
        company: [
          {
            "company": "蚂蚁金服",
            "image": "/mayi.jpg",
            "title": "Java",
            "salary":  "20-40K",
            "tags": ["杭州","3-5年","本科"]
          },
          {
            "company": "网易",
            "image": "/netease.jpg",
            "title": "资深Java开发工程师",
            "salary":  "25-50K",
            "tags": ["杭州","3-5年","本科"]
          },
          {
            "company": "滴滴出行",
            "image": "/didi.jpg",
            "title": "Java",
            "salary":  "25-50K",
            "tags": ["杭州","3-5年","本科"]
          },
          {
            "company": "同花顺",
            "image": "/tonghuashun.jpg",
            "title": "Java-web开发工程师",
            "salary":  "15-30K",
            "tags": ["杭州","3-5年","本科"]
          },
          {
            "company": "天猫",
            "image": "/tmall.jpg",
            "title": "Java",
            "salary":  "30-50K",
            "tags": ["杭州","3-5年","本科"]
          },
          {
            "company": "杭州海康威视",
            "image": "/hik.jpg",
            "title": "Java项目经理",
            "salary":  "18-25K",
            "tags": ["杭州","5-10年","本科"]
          }
        ],
        
        index_categories: null,
        title: '杭州Java招聘」 - BOSS直聘'
      }
    },
  // created() {
  //   fetch("http://127.0.0.1:3000/api/list_filter.json")
  //   .then((res) => {
  //     return res.json()
  //   })
  //   .then((data) => {
  //     vm.filter = data
  //   })

  //   fetch("http://127.0.0.1:3000/api/list_company.json")
  //   .then((res) => {
  //     return res.json()
  //   })
  //   .then((data) => {
  //     vm.company = data
  //   })
  // },
  methods: {
    changeCategories(index) {
      if(this.index_categories === index) {
        this.index_categories = null
      }
      else {
        this.index_categories = index
      }
    },
    changeOptions(index1, index2) {
      this.index_options[index1] = index2
    }
  },
  computed: {
    index_options() {
      return new Array(this.filter.length).fill(0)
    }
  },
  head() {
    return {
      title: this.title
    }
  }
}
</script>

<style>
.list-header {
  padding: 0.8rem 1rem;
}

.list-header img {
  height: 1.2rem;
}
.list-header form {
  width: 100%;
}
.list-header form .inner {
  width: 100%;
  background: #f5f8f9;
  margin: 0 1rem;
  line-height: 1.7rem;
  border-radius: 2rem;
  padding: 0 1rem;
}
.list-header form input {
  border: none;
  width: 80%;
  background: transparent;
  outline: none;
  color: #7e8793;
}
.list-header form button {
  border: none;
  background: none;
  font-size: 0.9rem;
  color: #5bd4c7;
  flex-shrink: 0;
  padding: 0;
}

.filter {
  padding: 0.5rem 1rem;
  border: 1px solid #f5f8f9;
}
.filter dl, .filter dd {
  margin: 0;
}
.filter dt {
  font-size: 0.8rem;
}
.filter .active dt {
  color: #333;
}
.filter dt:after {
  content: '';
  display: inline-block;
  width: 4px;
  height: 4px;
  border: 1px solid #999;
  margin-left: 0.5rem;
  border-style: solid none none solid;
  transform: rotate(225deg);
  transform-origin: 2px 1px;
  transition: all 1s;
}
.filter .active dt:after {
  transform: rotate(45deg);
}
.filter dd {
  display: none;
}
.filter .active dd {
  display: block;
  background: rgba(0,0,0,0.3);
  width: 100%;
  height: 100vh;
  position: absolute;
  top: 88.6px;
  left: 0;
}
.filter .active dd ul {
  margin: 0;
  padding: 0;
  background: #fff;
  
}
.filter .active dd li {
  line-height: 3.5rem;
  text-indent: 1rem;
  list-style: none;
  color: #aaa;
}
.filter .active dd li.active {
  background: #f5f8f9;
  color: #333;
}


.job-list {
  margin: 0;
  padding: 0;
}
.job-item {
  margin: 1rem;
  padding-bottom: 1rem;
  color: #7e8793;
  text-decoration: none;
  border-bottom: 1px solid #f5f8f9;
}
.job-item > img {
  height: 3.5rem;
  border-radius: 0.3rem;
}
.job-item .text {
  width: 100%;
  margin-left: 1rem;
}
.job-item .title, .job-item .company{
  color: #333;
  font-size: 0.9rem;
}
.job-item .company {
  color: #333;
  font-size: 0.8rem;
  margin: 0.2rem 0;
}
.job-item .salary {
  font-size: 1.2rem;
  color: #fc6c38;
}
.job-item .props {
  font-size: 0.8rem;
}
.job-item .props span {
  margin-right: 0.5rem;
}
</style>

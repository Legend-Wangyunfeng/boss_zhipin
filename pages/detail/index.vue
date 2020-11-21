<template>
  <div class="container" id="app">
    <div class="top-bar flex padded">
      <img src="/logo.png" alt="">
      <form action="" class="flex">
        <input type="text" placeholder="搜索职位">
        <button class="search-icon"></button>
      </form>
    </div>

    <div class="job-info padded">
      <div class="title flex">
        <span>{{job.title}}</span>
        <span class="salary">{{job.salary}}</span>
      </div>
      <div class="props flex">
        <div class="items flex">
          <template v-for="(tag, index) in job.tags">
            <i v-if="index > 0" :key="tag"></i>
            {{tag}}
          </template>
        </div>
        <div>
          发布于{{job.date}}
        </div>
      </div>
      <div class="tags">
        <span v-for="label in job.labels" :key="label">{{label}}</span>
      </div>
    </div>

    <div class="user-info flex padded" v-if="job.user">
      <img :src="job.user.avatar" alt="">
      <div class="info">
        <div class="name flex">
          <span>{{job.user.name}}</span>
          <span class="like">
            <img src="/link-like.png" alt="">
            感兴趣
          </span>
        </div>    
        <div class="desc">{{job.user.title}}</div>
      </div>
      <button class="btn" type="button">立即沟通</button>
    </div>
    <div class="job-detail padded" v-if="job.company">
      <h3>职位描述</h3>
      <div class="text" v-html="job.body">
      </div>
      <h3>公司介绍</h3>
      <div class="text" v-html="job.company.body">
        
      </div>
      <h3>工商信息</h3>
      <div class="text">
        <p>{{job.company.full_name}}</p>
        <table>
          <tr>
            <th>法人代表：</th>
            <td>{{job.company.props.法人代表}}</td>
            <th>注册资本：</th>
            <td>{{job.company.props.注册资本}}</td>
          </tr>
          <tr>
            <th>成立时间：</th>
            <td>{{job.company.props.成立时间}}</td>
            <th>经营状态：</th>
            <td>{{job.company.props.经营状态}}</td>
          </tr>
        </table>
        <p class="grey"><small>数据来源：企查查</small></p>
      </div>
      <h3>工作地址</h3>
      <div class="map"></div>
    </div>
    
    <div class="company-info flex padded" v-if="job.company">
      <img :src="job.company.logo" alt="">
      <div class="info">
        <div class="name flex">
          <span>{{job.company.name}}</span>
          <button class="btn" type="button">关注该公司</button>
        </div>
        <div class="desc">{{job.company.full_name}}</div>
        <div class="tags">
          <template v-for="(tag, index) in job.company.tags">
            <i v-if="index > 0" :key="tag"></i>
            {{tag}}
          </template>
        </div>
      </div>
    </div>

    <div class="related-jobs padded">
      <h3>相似职位</h3>
      <ul>
        <li v-for="related_job in job.jobs" :key="related_job.company">
          <a href="" class="job-item flex">
            <img :src="related_job.logo" alt="">
            <div class="text">
              <div class="title flex">{{related_job.title}}<span class="salary">{{related_job.salary}}</span></div>
              <div class="flex">
                <div class="company">{{related_job.company}}</div>
                <button class="btn" type="button">立即沟通</button>
              </div>           
            </div>
          </a>
        </li>

        
      </ul>
    </div>

    <div class="related-companies padded">
      <h3>城市招聘：</h3>
      <div class="tags">
        <a href="" v-for="city in job.cities" :key="city.id">{{city.name}}招聘</a>
      </div>
    </div>

    <div class="job-footer breadcrumb-nav">
      <template v-for="(path, index) in job.pathes">
        <i v-if="index > 0 "></i>
        <a href="">{{path.title}}</a>
      </template>
      
    </div>
  </div>  
</template>

<script>
export default {
  data() {
    return {
      job: {
        "head_title": "「Java招聘」_蚂蚁金服招聘-BOSS直聘",
        "title": "Java",
        "salary":  "20-40K",
        "tags": ["杭州","3-5年","本科"],
        "date": "2020-10-26",
        "labels": ["Java", "中间件", "后端开发"],
        "user": {
          "id": 1,
          "avatar": "/avatar_14.png",
          "name": "李先生",
          "title": "蚂蚁金服 · 技术专家"
        },
        "body": "1、 理解商户业务，识别需求，用数据赋能商业经营。<br>2、 参与系统架构设计和优化，独立完成系统分析文档的撰写；<br>3、 沉淀有价值的商户数据资产，以数据化的方式联通商户、平台与消费者，打造一站式商户服务体系。<br>4、 有主人公意识和数据感觉，熟悉hadoop，hbase，spark等大数据解决方案。",
        "company": {
          "name": "蚂蚁金服",
          "full_name":"蚂蚁金服（杭州）网络技术有限公司",
          "tags": ["互联网金融", "D轮及以上", "10000人以上"],
          "logo": "/mayi.jpg",
          "body": "蚂蚁金融服务集团（以下称“蚂蚁金服”）起步于2004年成立的支付宝。2014年10月，蚂蚁金服正式成立。蚂蚁金服以“让信用等于财富”为愿景，致力于打造开放的生态系统，通过“互联网推进器计划”助力金融机构和合作伙伴加速迈向“互联网+”，为小微企业和个人消费者提供普惠金融服务。 蚂蚁金服旗下有支付宝、余额宝、招财宝、蚂蚁聚宝、网商银行、蚂蚁花呗、芝麻信用、蚂蚁金融云、蚂蚁达客等子业务板块。",
          "props": {
            "法人代表": "程立",
            "注册资本": "1000万元人民币",
            "成立时间": "2013-10-22",
            "经营状态": "存续"
          }
        },
        "jobs": [
        {
          "company": "滴滴出行",
          "title": "Java",
          "salary":  "25-50K",
          "date": "2020-10-26T06:03:58.439Z",
          "logo": "/didi.jpg"       
        },
        {
        "company": "网易",
        "title": "资深Java开发工程师",
        "salary":  "25-50K",
        "logo": "/netease.jpg",
        "date": "2020-10-26T06:03:58.439Z"
        }
        ],
        "cities": [
          {"id":1, "name": "博尔塔拉"},
          {"id":2, "name": "赤峰"},
          {"id":3, "name": "青岛"},
          {"id":4, "name": "葫芦岛"},
          {"id":5, "name": "乐山"},
          {"id":6, "name": "信阳"},
          {"id":7, "name": "泰州"}
        ],
        "pathes": [
          {"title": "首页", "url": "/"},
          {"title": "杭州招聘·Java招聘", "url": "/"},
          {"title": "杭州Java招聘", "url": "/"},
          {"title": "蚂蚁金服Java招聘", "url": "/"}
        ]
      }
    }
    
  },
  head() {
    return {
      title: this.job.head_title
    }
  }
  // created() {
  //   fetch("http://127.0.0.1:3000/api/detail.json")
  //   .then((res) => {
  //     return res.json()
  //   })
  //   .then((data) => {
  //     vm.job = data
  //   })
  // }
}
</script>

<style>

/* detail */
.top-bar img {
  height: 1rem;
}
.top-bar form {
  width: 40%;
  border: 1px solid #5bd4c7;
  border-radius: 2rem;
  padding: 0 0.5rem;
}
.top-bar form input {
  border: none;
  background: none;
  line-height: 1.5rem;
  width: 80%;
  color: #aaa;
  font-size: 0.9rem;
  outline: none;
}
.top-bar form button {
  border: none;
  background: url('/icons.png') no-repeat top center;
  background-size: 100% auto;
  display: inline-block;
  width: 1rem;
  height: 1rem;
}

.job-info {
  background-color: #62d5c8;
  color: #fff;
}
.job-info .title {
  font-size: 1.2rem;
}
.job-info .props {
  font-size: 0.8rem;
  margin: 0.5rem 0;
}
.job-info .props .items i {
  display: inline-block;
  width: 1px;
  height: 0.8rem;
  background-color: #fff;
  margin: 0 0.5rem;
}
.job-info .tags span {
  border: 1px solid #fff;
  padding: 0.2rem 0.5rem;
  border-radius: 2rem;
  font-size: 0.75rem;
  margin-right: 0.3rem;
}

.user-info {
  background-color: #eefbf9;
}
.user-info > img {
  height: 3.5rem;
  border-radius: 3.5rem;
}
.btn {
  border: none;
  font-size: 0.9rem;
  padding: 0.5rem 1.2rem;
  border-radius: 2rem;
}
.user-info > button {
  background: #62d5c8;
  color: #fff;
  flex-shrink: 0;
}
.user-info .name {
  color: #333;
}
.user-info .name .like {
  font-size: 0.8rem;
  color: #fb7042;
}
.user-info .desc {
  font-size: 0.8rem;
  color: #aaa;
  margin-top: 0.5rem;
}
.user-info .info {
  width: 40%;
  margin: 0 1rem;
}

.job-detail h3{
  color: #333;
  font-size: 1rem;
  position: relative;
}
.job-detail h3:after {
  content: '';
  width: 1rem;
  height: 1px;
  display: inline-block;
  background-color: #62d5c8;
  position: absolute;
  top: 1.8rem;
  left: 0;
}
.job-detail .text {
  font-size: 0.95rem;
  line-height: 1.6rem;
}
.job-detail .text table {
  border: 1px solid #ebecef;
  padding: 0.7rem 0.3rem;
  font-size: 0.75rem;
}
.job-detail .text th {
  font-weight: normal;
  width: 6rem;
  color: #9fa3b0;
}
.job-detail .text td {
  width: 8rem;
}

.company-info {
  background: #eefbf9;
}
.company-info img {
  height: 3.5rem;
  border-radius: 3.5rem;
}
.company-info .info {
  width: 100%;
  margin-left: 1rem;
}
.company-info .info .name {
  color: #333;
}
.company-info .info .name button{
  background: #62d5c8;
  color: #fff;
}
.company-info .info .desc {
  font-size: 00.8rem;
  color: #333;
}
.company-info .info .tags {
  margin-top: 0.5rem;
  font-size: 0.75rem;
}
.company-info .info .tags i{
  display: inline-block;
  height: 0.8rem;
  width: 1px;
  background-color: #ebecef;
}

.related-jobs h3{
  font-size: 1rem;
  color: #7e8793;
  font-weight: normal;
}
.related-jobs ul {
  list-style: none;
  padding-left: 0;
}
.related-jobs ul li>a {
  border: none;
  margin: 0;
  border-top: 1px solid #ebecef;
  padding: 1rem 0;
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
.related-jobs .btn {
  border: 1px solid #62d5c8;
  background-color: #fff;
  color: #62d5c8;
  padding: 0.4rem 1.2rem;
  margin-top: 0.2rem;
}

.related-companies h3{
  font-size: 1rem;
  color: #7e8793;
  font-weight: normal;
}
.related-companies .tags a{
  color: #7e8793;
  text-decoration: none;
  font-size: 0.8rem;
  margin: 0 0.7rem 0.3rem 0;
}

.job-footer {
  border-top: 1px solid #ebecef;
  margin: 0 1rem;
  padding: 1rem 0;
  line-height: 1.5rem;
}
.job-footer a{
  color: #7e8793;
  text-decoration: none;
  font-size: 0.75rem;
  margin: 0 0 0.3rem 0;
}
.job-footer i {
  display: inline-block;
  width: 8px;
  height: 8px;
  border: 1px solid #9fa3b0;
  border-style: solid none none solid;
  transform: rotate(135deg);
}
</style>
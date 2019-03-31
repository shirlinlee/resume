<template>
<div class="resume">
  <div class="leftCol m_box">
    <div class="shadow"></div>
    <div class="heading" id="myselfpic">
    </div>
    
    <div class="item">
      <div class="icon">
        <i class="material-icons">account_circle</i>
      </div>
      <div class="text">
        <ul>
          <li> {{person.birth.year}} 出生</li>
        </ul>
      </div>
    </div>

    <div class="item">
      <div class="icon">
        <i class="material-icons">location_city</i>
      </div>
      <div class="text">
        <ul>
          <li>現居 {{person.contact.city}}</li>
        </ul>
      </div>
    </div>

    <a :href="contactLinks.phone">
      <div class="item">
        <div class="icon">
          <i class="material-icons">phone</i>
        </div>
        <div class="text">
          {{person.contact.phone}}
        </div>
      </div>
    </a>

    <a :href="contactLinks.email">
      <div class="item">
        <div class="icon">
          <i class="material-icons">email</i>
        </div>
        <div class="text">
          {{person.contact.email}}
        </div>
      </div>
    </a>

    <a v-if="person.contact.github" :href="contactLinks.github" target="_blank">
      <div class="item">
        <div class="icon">
          <i class="fa fa-github"></i>
        </div>
        <div class="text">
          <span>{{person.contact.github}}</span>
        </div>
      </div>
    </a>

  </div>

  <div class="rightCol">
    <div class="title">
      <h2>{{person.name.first}} {{person.name.last}}</h2>
      <h3>{{person.position}}</h3>
      <div v-html="person.about"></div>
    </div>

    <div class="section-headline">{{ lang.experience }}</div>
    <div class="block" v-for="experience in person.experience" :key="experience.company">
      <div class="block-helper"></div>
      <h3 class="headline">{{experience.position}} - {{experience.company}}</h3>
        <div class="subheadline">{{experience.timeperiod}}</div>
        <p class="info">
          {{experience.description}}
        </p>
    </div>
    <div class="section-headline">{{ lang.education }}</div>
    <div class="block" v-for="education in person.education" :key="education.degree">
      <div class="block-helper"></div>
      <div class="headline">{{education.degree}}</div>
      <p class="info">
        {{education.timeperiod}} - {{education.description}}
      </p>
    </div>

    <div class="section-headline"> {{ lang.skills }}</div>
    <div class="skill" v-for="skill in person.skills" :key="skill.name">
      <div class="right">
        <span>{{skill.name}}&nbsp;</span>
        <div class="progress">
          <div class="determinate" :style="'width: '+skill.level+'%;'">
            <i class="fa fa-circle"></i>
          </div>
        </div>
      </div>
    </div>

    <div class="section-headline">近期專案</div>
    <div class="block" v-for="(c,index) in person.case" :key="index">
      <div class="headline"><font>[ {{c.tag}} ] </font> {{c.name}}</div>
      <a class="info" :href="c.link" target="_blank">
        {{c.link}}
      </a>
      <ul class="tag_wrapper">
        <li v-for="sk in c.skill" :key="sk">{{sk}}</li>
      </ul>
    </div>

 

  </div>

  <div style="clear:both;"></div>
</div>
</template>

<script>
import Vue from 'vue';
import { getVueOptions } from './options';
const name = 'material-dark';

export default Vue.component(name, getVueOptions(name));
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="less" scoped>
.resume {
  font-family:'Roboto' !important;
  background:#eee;
  padding-bottom: 40px;
}
a {
  cursor:pointer;
}
.description-personal {
  margin-left:20px;
  margin-top:20px;
  padding-right:40px;
  text-align:justify;
  font-family:Roboto;
}
.title {
  // right:25px;
  // padding-left:0;
  // padding-right:20px;
  // padding-top:20px;
  // bottom:25px;
  width: 96%;
  display: inline-block;
  @media only screen and (max-width: 700px) {
    width: 100%;
  }
  h2 {
    text-transform:uppercase;
    display:block;
    font-size:1.9em;
    -webkit-margin-before:1em;
    -webkit-margin-after:1em;
    -webkit-margin-start:0;
    -webkit-margin-end:0;
    color: rgb(22, 103, 123);
    padding-top:0;
    margin-top:20px;
    letter-spacing:2px;
    line-height: 1.7;
    font-weight:400;
    margin-bottom: 0;
  }
  h3 {
    font-size:1em;
    color: #b4b4b4;
  }
  div {
    font-size: 14px;
    color: rgba(0, 0, 0, 0.7);
    font-weight: 400;
    display: block;
    line-height: 1.5;
    margin-top: 15px;
    letter-spacing: 2px;
  }
}
.section-headline {
  text-transform:uppercase;
  font-weight:500;
  letter-spacing:3px;
  font-size:15px;
  // opacity:0.8;
  padding-left:20px;
  margin-top:40px;
  margin-bottom:10px;
  color:#16687b;
  position: relative;
  
  &:before{
    content: '';
    width: 7px;
    height: 7px;
    display: block;
    position: absolute;
    left: 0;
    top: 5px;
    background-color: #16687b;
  }
}
.c {
  clear:both;
}
li {
  margin:0;
  padding:0;
  list-style-type:none;
  padding-top:9px;
}
ul {
  margin:0;
  padding:0;
  list-style-type:none;
}
p {
  margin-top:0;
  margin-bottom:25px;
  font-family:'Roboto', sans-serif;
  font-weight:300;
  font-size:10pt;
  line-height:17pt;
}
.m_box {
  box-shadow:0 2px 5px 0 rgba(0,0,0,0.16), 0 2px 10px 0 rgba(0,0,0,0.12);
}
.fa, .material-icons {
  display:inline-block;
  font-style:normal;
  font-weight:normal;
  line-height:1.1;
  -webkit-font-smoothing:antialiased;
  -moz-osx-font-smoothing:grayscale;
  font-size:20px;
}
div{
  box-sizing: border-box;
}
h1, h3, h5, h6 {
  font-weight:400;
  margin:0;
}
h2 {
  font-weight:400;
  font-weight:500;
  margin:0;
  margin:0;
  font-size:22pt;
  line-height:37pt;
}
h4 {
  font-weight:400;
  margin:0;
  font-size:12pt;
  line-height:20pt;
  opacity:1;
}
.rightCol {
  width:63.5%;
  // height:100%;
  float:right;
  box-sizing: border-box;

  @media only screen and (max-width: 700px) {
    width: 100%;
    float: none;
    display: inline-block;
    padding: 0 20px;
  }
  // display:flex;
  // flex-direction:column;
  .block {
    box-sizing: border-box;
    width:96%;
    position:relative;
    background-color:#ffffff;
    padding:20px;
    margin-top:5px;
    margin-bottom:5px;
    display:inline-block;
    box-shadow:0 2px 5px 0 rgba(0,0,0,0.16), 0 2px 10px 0 rgba(0,0,0,0.12);
    @media only screen and (max-width: 700px) {
      width: 100%;
    }
    .headline {
      font-weight:400;
      display:block;
      font-size:15px;
      color:rgba(0,0,0,0.870588);
      font {
        color: #444;
        font-weight:300;
        padding-right: 4px;
      }
    }
    .subheadline {
      color:rgba(0,0,0,0.7);
      display:block;
      font-size:12px;
      padding-top: 3px;
      font-weight:300;
    }
    .info {
      font-size:14px;
      font-weight: 300;
      color:rgba(0,0,0,0.870588);
      margin-bottom:0;
      padding-top:20px;
      position: relative;
      display: inline-block;
      text-decoration: none;
      &:after{
        content: '';
        position: absolute;
        width: 30px;
        height: 1px;
        background-color: #9dc6c4;
        top: 9px;
        left: 0;
      }
    }
     a.info{
      white-space: nowrap;
      text-overflow: ellipsis;
      width: 100%;
      overflow: hidden;
        &:hover{
          color: #16687b;
        }
    }
    
    .icon {
      width:16%;
      float:left;
      margin-left:0;
      .fa, .material-icons {
        text-align:center;
        display:block;
        font-size:30pt;
      }
    }
    .content {
      width:80%;
      position:absolute;
      height:96%;
      left:17%;
      padding-right:3%;
      text-align:left;
      // display:flex;
      // flex-direction:column;
      .item {
        border-bottom:1px solid #bdbdbd;
        flex:1;
        width:97%;
        // display:flex;
        // justify-content:center;
        // flex-direction:column;
        text-align:left;
        padding-top:0;
        span {
          color:#d8ab94;
          margin-top:0;
          font-size:10pt;
          line-height:16pt;
        }
        p {
          margin-top:5px;
        }
      }
      .item:last-of-type {
        border-bottom-style:none;
        border-bottom-style:none;
      }
    }
  }
}
.leftCol {
  position: fixed;
  width:33%;
  height:100vh;
  float:left;
  padding:0;
  text-align:left;
  color:#ffffff;
  color:rgba(255,255,255,0.9);
  background-color:#1b8299;
  overflow:hidden;
  display:block;
  @media only screen and (max-width: 700px) {
    position: relative;
    width: 100%;
    height: inherit;
    padding-bottom: 25px;
    
  }
  .section-headline {
    color:rgba(255,255,255,0.54);
  }
  a {
    color:rgba(255,255,255,0.9);
    text-decoration:none;
    &:hover {
      div{
        color: rgb(253, 159, 159);
      }
    }
  }
  .heading {
    background-color:white;
    background-repeat:no-repeat;
    background-size:cover;
    background-position:center;
    position:relative;
    margin: 25px auto;
    border-radius: 50%;
    width: 20vw;
    height:20vw;
    @media only screen and (max-width: 700px) {
      margin: 25px auto 10px;

    }
  }
  .item {
    width:100%;
    margin-top:13px;
    float:left;
    .fa, .material-icons {
      display:inherit;
      text-align:center;
    }
    .icon {
      width:18%;
      float:left;
    }
    .text {
      float:right;
      width:80%;
      padding-right:10%;
      padding-top:0;
      display:block;
      font-size:15px;
      font-weight:300;
    
      li {
        padding-top:0;
        display:block;
        font-size:16px;
        font-weight:300;
      }
    }
    span {
      font-weight:300;
    }
    
  }
  .item.last .text {
    border-bottom-style:none;
    padding-bottom:0;
  }
}
#myselfpic {
  background-image:url('../../resume/me.jpg');
  color:black;
  box-shadow: 0 0 0 6px rgba(255,255,255,.1), 0 0 0 12px rgba(255,255,255,.1);
}
#githubIcon {
  width:25px;
  padding-left:17px;
}
.skill {
  // clear:both;
  width:45%;
  margin-right: 5%;
  display: inline-block;
  padding-top:10px;
  div{
    font-size: 15px;
    font-weight: 300;
  }
  .left {
    float:left;
    width:10%;
    padding-top:3px;
    i:nth-child(2) {
      float:left;
      padding-top:4px;
    }
  }
  .right {
    // float:right;
    // width:93%;
  }


  &:nth-child(even){
    margin-right: 0;

  }
}
.progress {
  float:left;
  position:relative;
  height:4px;
  display:block;
  width:100%;
  background-color:#fff;
  border-radius:2px;
  margin:0.5rem 0 1rem;
  overflow:visible;
  margin-bottom:10px;
  .determinate {
    background-color:rgba(22, 104, 123, 0.39);
    position:absolute;
    top:0;
    bottom:0;
    .fa, .material-icons {
      font-size:13px;
      position:absolute;
      top:-4px;
      right:-2px;
      margin-left:50%;
      color:#16687b;
    }
  }
}
.tag_wrapper{
  padding: 15px 0 0;
  li {
    display: inline-block;
    line-height: 20px;
    padding: 0 8px;
    margin: 0 8px 8px 0;
    // color:#16687b;
    color: #fff;
    font-size: 14px;
    font-weight: 300;
    // border: solid 1px #16687b;
    border-radius: 4px;
    background-color: rgb(253, 159, 159);
  }

  }
</style>

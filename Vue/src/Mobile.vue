<template>
  <div id="app">
    <StyleEditor ref="styleEditor" :code="currentStyle"></StyleEditor>
    <ResumeEditor ref="resumeEditor" :markdown="currentMarkdown" :enableHtml="enableHtml"></ResumeEditor>
  </div>
</template>

<script>
  import StyleEditor from './components/StyleEditor'
  import ResumeEditor from './components/ResumeEditor'
  import './assets/reset.css'

  export default {
    name: 'app',
    components: {
      StyleEditor,
      ResumeEditor
    },
    data() {
      return {
        interval: 5,
        currentStyle: '',
        enableHtml: false,
        fullStyle: [
          `/*
* Inspired by http://strml.net/
* Hi, This is Lan Liang.
* Below is my CV Profile.
*/

/* filter */
* {
  transition: all .2s;
}
/* background color */
html {
  color: rgb(222,222,222);
  background: rgb(0,43,54);
}
/* border */
.styleEditor {
  padding: .5em;
  border: 1px solid;
  overflow: auto;
  width: 90vw;
  margin: 2.5vh 5vw;
  height: 90vh;
}
/* height */
.styleEditor {
  height: 45vh;
}
/* highlight */
.token.selector{
  color: rgb(133,153,0);
}
.token.property{
  color: rgb(187,137,0);
}
.token.punctuation{
  color: yellow;
}
.token.function{
  color: rgb(42,161,152);
}

/* 3d */
html{
  perspective: 1000px;
}
.styleEditor {
  position: fixed; left: 0; top: 0;
  transform: rotateX(-10deg) translateZ(-50px) ;
}

/* editor */
.resumeEditor{
  position: fixed;
  top: 50%; left: 0;
  padding: .5em;  margin: 2.5vh;
  width: 95vw; height: 45vh;
  border: 1px solid;
  background: white; color: #222;
  overflow: auto;
}
/* CV */


`,
          `
/*convert markdown to HTML
 *HTML styles
*/
`, `
.resumeEditor{
  padding: 2em;
}
.resumeEditor h2{
  display: inline-block;
  border-bottom: 1px solid;
  margin: 1em 0 .5em;
}
.resumeEditor ul,.resumeEditor ol{
  list-style: none;
}
.resumeEditor ul> li::before{
  content: '•';
  margin-right: .5em;
}
.resumeEditor ol {
  counter-reset: section;
}
.resumeEditor ol li::before {
  counter-increment: section;
  content: counters(section, ".") " ";
  margin-right: .5em;
}
.resumeEditor blockquote {
  margin: 1em;
  padding: .5em;
  background: #ddd;
}
`],
        currentMarkdown: '',
        fullMarkdown: `Lan Liang
====

Location: Singapore

Software Engineer/Architect/Technical Consultant

Skill set
====
Data Base
----
  - RDBMS
  - noSQL
----
Backend
----
  - Telco Messaging (China mobile)
  - HR System
  - Device Management System
  - AudoCAD plugin
  - Intellectual Property System 
  - Online Logistic Platform
  - Ticketing System
  - Bus System
  - Video talk/Facial Recognition System
  - Visitor Management System
  - Surveillance System 

Front End
----
  - Web Frontend
  - Mobile(Native App, Xamarin, Codorva)

Projects
----
  - Singapore Capital land mall surveillance System
  - PUB Visitor Management
  - Singapore SMRT Buscaptain System
  - www.Zyllem.com (B2C C2C Logistic system)
  - M1 Shop
  - Ip2SG 
  - Sentosa Ticketing System
  - Feinno Messaging (Backend, Api)
  - Hongye AutoCAD Plugin
  - Huawei Device management
  - Digital China HR System

Languages/Framework
----
  - Microsoft Technology: MFC, Winform , WPF, Asp.Net MVC, MSMQ, WCF, MS SQL Server, Entity Framework, MEF, Rx, Azure(App Service, Storage)
  - JavaScript: HandlebarJS, AngularJS, ReactJS, typescript, web socket
  - Java: Android, SQLite, okHttp
  - Node.js: express, restify
  - Python: Django, Flask, pandas, numpy, matplotlib
  - DB: SQLServer, Oracle, MongoDB, redis, PostgreSQL
  - WebServer: IIS, apache, nginx
  - OS: Windows, Ubuntu
  - Swift
  - Video/Audio: OpenCV, emguCV, ffmpeg
  - Others: JIRA, trello, git

Working Experience
----

1. Certis Technology Singapore PTE LTD |Nov 2017 - Now
2. NEC Asia Pacific PTE LTD |Jan 2016- Nov 2017
3. Smart Communities PTE LTD |Dec 2014 - Jan 2016
4. Keritos PTE LTD |Aug 2014 - Dec 2014
5. Comtel Solutions PTE LTD |Nov 2013 - Aug 2014
6. ITCAN PTE LTD |Dec 2012 - Nov 2013
7. Working at beijing |Jul 2010 - Dec 2012

Education
----
Beihang University Beihai college (Software Engineering) Degree

Links
----
* [GitHub](https://github.com/iorilan)
* [Technical Blog](http://blog.csdn.net/liang_lan)
* [Microsoft MVP] (https://mvp.microsoft.com/en-us/PublicProfile/5000709?fullName=Liang%20Lan)
* [Mastering Object-oriented Python](https://www.amazon.com/Python-x9762-x5411-x5BF9-Chinese-ebook/dp/B01DU00EMA)
* [Leetcode](https://leetcode.com/lanliang/)

Contact
----
* qq/wechat：274559465
* WhatsApp:91390681

Thank you
----
* Oct 2006.I still remember when I wrote my first line of code in C language .which was a command line game .I loved programming .sine then i could not stop programming and playing with my toys specially games(C# CRUD system, LAN chatting, J2me car game, WPF terix,javascript snake...)
* Sep 2009.Thanks all help I got from my intern company (jeemoo.net), where I build up my programming skill .and I finished my first project huaxiaacc.com with team :a online studying and certifying system for accountants .
* 
Mar 2011. after graduted , I choosed to be a .Net developer .I luckily joined the 2nd largest messaging software company :feinno (a product of china mobile).I learned how to handle high volume of requests ,and distributed service (now we call it micro-service) architecture .and I played a lead role .
* June 2011. I realized the importance of blogging for a programmer and I started my own (blog.csdn.net/liang_lan). I just write down what i don't konw and what i learned .
* Sep 2012. Started my career at Singapore .where I build systems for different domains :government, telco, ticking, casino, logistics, public transport, surveillance...
* April 2014. I was awarded as Microsoft .Net MVP. blog subscriber 4000+, PV 1m. many thanks to MS, my lead :Lina and Kris .
* Dec 2015. Started my role as Technical Consultant. since when i stopped my life not only like sitting down wearing a big headset and coding quietly but joined different conferences, make tech decisions and serve customers .and the same year I played my first architect role .Thanks my NEC colleagues. 
* I like MS technology ,and i love open source .I believe OpenSource is where the community to make the technology grow stronger and become mature. after went through many languages and frameworks: C, MFC, Winform, WPF, java, python, swift, OO patterns, algorithm, functional programming ,nodeJs, AspNet MVC, EF, flask, Django ..what I kept in mind are :code readability, testability, high cohesion.
* Technology changed fast .the 3 steps I kept in my minds are :build it . serve more clients(requests). make it smart(AI). I'd choose the technology stack what team comfortable with and we could afford the risk on the decision we made .whether it's a micro-service or monolithic ,mongoDB or MySQL,nodeJs or aspnet MVC, redis or RibbitMQ or ZeroMQ or kafka... as long as i could evolve my software with the 3 steps I will go for it .

`
      }
    },
    created() {
      this.makeResume()
    },

    methods: {
      makeResume: async function () {
        await this.progressivelyShowStyle(0)
        await this.progressivelyShowResume()
        await this.progressivelyShowStyle(1)
        await this.showHtml()
        await this.progressivelyShowStyle(2)
      },
      showHtml: function () {
        return new Promise((resolve, reject) => {
          this.enableHtml = true
          this.$nextTick(() => {
            this.$refs.resumeEditor.goTop()
          })
          resolve()
        })
      },
      progressivelyShowStyle(n) {
        return new Promise((resolve, reject) => {
          let interval = this.interval
          let showStyle = (async function () {
            let style = this.fullStyle[n]
            if (!style) { return }
            // count
            let length = this.fullStyle.filter((_, index) => index <= n).map((item) => item.length).reduce((p, c) => p + c, 0)
            let prefixLength = length - style.length
            if (this.currentStyle.length < length) {
              let l = this.currentStyle.length - prefixLength
              let char = style.substring(l, l + 1) || ' '
              this.currentStyle += char
              if (style.substring(l - 1, l) === '\n' && this.$refs.styleEditor) {
                this.$nextTick(() => {
                  this.$refs.styleEditor.goBottom()
                })
              }
              setTimeout(showStyle, interval)
            } else {
              resolve()
            }
          }).bind(this)
          showStyle()
        })
      },
      progressivelyShowResume() {
        return new Promise((resolve, reject) => {
          let length = this.fullMarkdown.length
          let interval = this.interval
          let showResume = () => {
            if (this.currentMarkdown.length < length) {
              this.currentMarkdown = this.fullMarkdown.substring(0, this.currentMarkdown.length + 1)
              let lastChar = this.currentMarkdown[this.currentMarkdown.length - 1]
              let prevChar = this.currentMarkdown[this.currentMarkdown.length - 2]
              if (prevChar === '\n' && this.$refs.resumeEditor) {
                this.$nextTick(() => this.$refs.resumeEditor.goBottom())
              }
              setTimeout(showResume, interval)
            } else {
              resolve()
            }
          }
          showResume()
        })
      }
    }
  }

</script>

<style scoped>
  #app {
    font-family: 'Avenir', Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    min-height: 100vh; position: relative;
  }

  html {
    min-height: 100vh;
  }
  *{
    box-sizing: border-box;
  }

</style>

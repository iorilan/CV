<template>
  <div id="app">
    <div id="content">
      <StyleEditor ref="styleEditor" :code="currentStyle"></StyleEditor>
      <ResumeEditor ref="resumeEditor" :markdown="currentMarkdown" :enableHtml="enableHtml"></ResumeEditor>
    </div>
    <div id="foot">
      <ThankEditor ref="thankEditor" :markdown="currentThankMarkdown" :enableHtml="enableHtml"></ThankEditor>
    </div>
  </div>
</template>

<script>
  import StyleEditor from './components/StyleEditor'
  import ResumeEditor from './components/ResumeEditor'
  import ThankEditor from './components/ThankEditor'
  import './assets/reset.css'

  export default {
    name: 'app',
    components: {
      StyleEditor,
      ResumeEditor,
      ThankEditor
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
  transition: all .1s;
}
/* background color */
html {
  color: rgb(222,222,222); background: rgb(0,64,64);
}
#content{
  height:70vh;
  margin:0;
}
#foot{
  height:29vh;
  margin:0;
}

/* border */
.styleEditor {
  padding: .5em;
  border: 1px solid;
  margin: .5em;
  overflow: auto;
  width: 50vw; height: 70vh;
  background: rgb(20,20,20);
}
/* code highlight */
.token.selector{ color: rgb(130,150,0); }
.token.property{ color: rgb(190,140,0); }
.token.punctuation{ color: yellow; }
.token.function{ color: rgb(40,160,150); }

/* 3D effect */
html{
  perspective: 1000px;
}
.styleEditor {
  position: fixed; left: 0; top: 0;
  -webkit-transition: none;
  transition: none;
  -webkit-transform: rotateY(10deg) translateZ(-100px) ;
          transform: rotateY(10deg) translateZ(-100px) ;
}

/* editor */
.resumeEditor{
  position: fixed; right: 0; top: 30;
  padding: .5em;  margin: .5em;
  width: 50vw; height: 70vh;
  border: 1px solid;
  background: rgb(200,200,200); color: #222;
  overflow: auto;
  -webkit-transition: none;
  transition: none;
  -webkit-transform: rotateY(-10deg) translateZ(-100px) ;
          transform: rotateY(-10deg) translateZ(-100px) ;
}
/* CV */
`, `
/*convert markdown to HTML
 *HTML styles
*/
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
`, `/*
 * 
 */
.thankEditor{
  position: fixed; left: 0; bottom: 0;
  padding: .5em;  margin: .5em; margin-top:.2em;
  font-size: .8em;
  width: 99vw; height: 28vh;
  border: 1px solid #ccc;
  background: rgb(10,10,10);
  color: rgb(0,200,0);
  overflow: auto;
}

.thankEditor ul,.thankEditor ol{
  list-style: none;
}
.thankEditor ul> li::before{
  content: '☞'; color: red;
  margin-right: .5em;
}
.thankEditor ol {
  counter-reset: section;
}
.thankEditor ol li::before {
  counter-increment: section;
  content: counters(section, "☞") " ";
  margin-right: .5em;
}
`],
        currentMarkdown: '',
        currentThankMarkdown: '',
        fullMarkdown: `Lan Liang
====

Location: Singapore

Software Engineer/Architect/Consultant

Skillset
====
Data Base
----
  - RDBMS
  - noSQL
----
Backend Languages/Frameworks
----
  - Web/Winform Application :Asp.Net 5, Asp.Net Core, Winform ,WPF, .Net Core ; nodeJS, Python Flask
  - Data Science :Python Dlib , Scikit Learn ; C# tensorflow ,ML.net, CGNS .
  - Message Broker. Redis, Kafka, zeroMQ
Front End
----
  - Web Frontend (Jquery, ReactJS, VueJS)
  - Mobile(Android[java,kotlin], IOS[swift], Xamarin, Codorva)
Protocol
----
  - Http/Https
  - WebSocket
  - TCPIP/UDP
  - RTSP/RTMP/HLS
Projects
----
  - Singapore Capitaland mall surveillance System (Facial Recognition)
  - PUB Visitor Management (FingerPrint)
  - Singapore SMRT Buscaptain System
  - www.Zyllem.com (B2C C2C Logistic system)
  - M1 Shop
  - Ip2SG 
  - Sentosa Ticketing System
  - Feinno Messaging (Backend, Api)
  - Hongye AutoCAD Plugin
  - Huawei Device management
  - Digital China HR System

Languages/Framework/DevOps
----
  - Microsoft Technology: MFC, Winform , WPF, Asp.Net MVC, .Net Core, MSMQ, WCF, MS SQL Server, Entity Framework, MEF, SignalR, Azure(App Service, Storage)
  - JavaScript: HandlebarJS, AngularJS, ReactJS, VueJS, Typescript
  - Java: Android, SQLite, okHttp
  - Node.js: express, restify
  - Python: Django, Flask, pandas, numpy, matplotlib
  - DB: SQLServer, MongoDB, PostgreSQL
  - WebServer: IIS, express, apache, nginx
  - OS: Windows, Ubuntu, CentOS
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
`, thanksMarkdown: `Thank you
----

* Oct 2006.I still remember when I wrote my first line of code in C language .which was a command line game .since when I loved programming .then i could not stop programming and kept building toys(C# CRUD system, Java, LAN chatting, Poke Game, J2me car game, WPF terix,javascript snake, JS super mario...)
* Sep 2009.Thanks all help I got from my intern company (jeemoo.net), where built up my programming skill in practise.that was where I finished my first project huaxiaacc.com with team :a online studying - exam - then certifying system for accountants in beijing.
* Mar 2011. Joined the 2nd largest Instant messaging software company :feinno (a product of china mobile).where I learned how to handle high volume of requests ,and how distributed service (now we call it micro-service) architecture works .
* June 2011. I realized the importance of blogging for a programmer and the impressed by the power of open source community influences software industry. I started my own blog (blog.csdn.net/liang_lan). I start with write down what i don't konw and what i have learned .that where get my CS foundation solid.
* Sep 2012. I started my career in Singapore .where I start build systems for different domains :government, telco, ticking, casino, logistics, public transport, surveillance...
* April 2014. 1st time I was awarded as Microsoft .Net MVP for the work i have done on open source & IT communities.my blog subscriber was 4000+, PV 1m+. many thanks to MS, my lead :Lina and Kris .
* Dec 2015. Started my role as Technical Consultant. since when I start make technical decisions with architects and facing customers .and the same year I played my first architect role .Thanks NEC colleagues.
* Mar 2016. the book [Mastering Object Oriented Python] translated had been published .thanks to hu jun ying and publisher .
* I like MS technology ,It is a great company always come with nice tools & frameworks make software development easier .and i love open source .it is where to verify the code and make technology stronger and become mature. after went through many languages and frameworks: C, VB, MFC, Winform, WPF, java, python, swift, OOP, AOP, FP ,nodeJs, AspNet MVC, EF, flask, Django ..the importants I think is :readability, testability, high cohesion, component.
* Technology changed fast .My 3 steps thinking for any projects :get it works and done it right. serve more clients(increase request per second). make it smart(introduce AI).
  `
      }
    },
    created() {
      this.makeResume()
    },

    methods: {
      makeResume: async function () {
        await this.progressivelyShowStyle(0);
        await this.progressivelyShowResume();
        await this.progressivelyShowStyle(1);
        await this.showHtml();
        await this.progressivelyShowStyle(2);
        await this.progressivelyShowThanks()
      },
      showHtml() {
        return new Promise((resolve, reject) => {
          this.enableHtml = true
          resolve()
        })
      },
      progressivelyShowStyle(n) {
        return new Promise((resolve, reject) => {
          let interval = this.interval
          let showStyle = (async function () {
            let style = this.fullStyle[n]
            if (!style) {
              return
            }
            // count first few chars
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
      },
      progressivelyShowThanks() {
        return new Promise((resolve, reject) => {
          let length = this.thanksMarkdown.length
          let interval = this.interval
          let showThanks = () => {
            if (this.currentThankMarkdown.length < length) {
              this.currentThankMarkdown = this.thanksMarkdown.substring(0, this.currentThankMarkdown.length + 1)
              let lastChar = this.currentThankMarkdown[this.currentThankMarkdown.length - 1]
              let prevChar = this.currentThankMarkdown[this.currentThankMarkdown.length - 2]
              if (prevChar === '\n' && this.$refs.thankEditor) {
                this.$nextTick(() => this.$refs.thankEditor.goBottom())
              }
              setTimeout(showThanks, interval)
            } else {
              resolve()
            }
          }
          showThanks()
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
  }

  html {
    min-height: 100vh;
  }

  * {
    box-sizing: border-box;
  }
</style>

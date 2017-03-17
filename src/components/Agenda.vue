<template lang="html">
  <svg>

    <line x1="1vw" y1="0" x2="1vw" y2="100vh"stroke-width="3" stroke="#95989A"/>

    <line x1="1vw" y1="30vh" x2="4vw" y2="30vh"stroke-width="2" stroke="#95989A"/>
    <line x1="1vw" y1="70vh" x2="4vw" y2="70vh"stroke-width="2" stroke="#95989A" class="opacity"/>
    <circle cx="1vw" cy="30vh" r="0.8vw":fill="color[ eventNow.Class ]" stroke="#95989A" stroke-width="3"/>
    <circle cx="1vw" cy="70vh" r="0.8vw":fill="color[ eventNext.Class ]" stroke="#95989A" stroke-width="3"/>

    <text x="5vw" y="31.5vh" fill="#95989A" class="time">{{ eventNow.Time }}</text>
    <text x="5vw" y="37.5vh" fill="#95989A" class="title">{{ eventNow.Name }}</text>
    <text x="5.2vw" y="42vh" fill="#95989A" class="subtitle">{{ eventNow.Detail }}</text>

    <text x="5vw" y="71.5vh" fill="#95989A" class="time opacity">{{ eventNext.Time }}</text>
    <text x="5vw" y="77.5vh" fill="#95989A" class="title opacity">{{ eventNext.Name }}</text>
    <text x="5.2vw" y="82vh" fill="#95989A" class="subtitle opacity">{{ eventNext.Detail }}</text>

  </svg>
</template>

<script>
var _ = require('lodash');
var Airtable = require('airtable');
var scheduleDB = new Airtable({apiKey: 'keyYBgDwHL1wU0BZh'}).base('appcs0kkOF4h36C7J');
var firstQuery = [];

export default {
  name: 'agenda',
  data: function(){
    return{
      items: [],
      eventNow: {
        class: 'events',
        Time: 'Now',
        Name: 'Hacking',
        Detail: '-',
      },
      eventNext: {
        class: 'fun',
        Time: '時間二',
        Name: '標題二',
        Detail: '副標二',
      },
      color: {
        agenda: '#62C7FC',
        events: '#4EF27A',
        fun:    '#FCFC62',
        food:   '#FC6291',
      },
    }
  },

  created() {

    // Save Airtable data first
    this.getRecords()

    // Update agenda if need
    let updateAgenda = setInterval(() => {
      this.checkNext()
    }, 5000)

  },

  methods:{
    checkNext(){
      var i
      for(i=0; i<this.items.length; i++){
        var eventTime = new Date(this.items[i].start)
        if(eventTime > Math.trunc((new Date()).getTime())){
          this.eventNow = this.items[i]
          console.log('eventNow:', this.eventNow.Name);
          this.eventNext = this.items[i+1]
          console.log('eventNext: ', this.eventNext.Name);
          return
        }
      }
    },

    getRecords(){
      console.log('getRecords()...');
      let items = []
      scheduleDB('小黑客松-流程').select({
        maxRecords: 20,
        view: "Main View"
      }).eachPage(function page(records, fetchNextPage) {

        items = items.concat(_.map(records, (record) => _.set(record.fields, 'id', record.id)));

        fetchNextPage();
      }, (err) => {
        if (err) { console.error(err); return; }
        this.items = items
      });
    },
  },
}
</script>

<style lang="css">
svg{
  width: inherit;
  height: inherit;
}
.time{
  /*font-size: 1.2em;*/
  font-size: 4vh;
}
.title{
  /*font-size: 1.5em;*/
  font-size: 5vh;
}
.subtitle{
  /*font-size: 1em;*/
  font-size: 2.5vh;
}
.opacity{
  opacity: 0.5;
}
</style>

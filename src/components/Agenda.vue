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
let twoDigits = number => number <= 99 ? ("0"+number).slice(-2) : number;

export default {
  name: 'agenda',
  data: function(){
    return{
      items: [],
      eventNow: {
        class: 'events',
        Time: 'Fetching...',
        Name: '...',
        Detail: '...',
      },
      eventNext: {
        class: 'fun',
        Time: 'Fetching...',
        Name: '...',
        Detail: '...',
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

    // Save Airtable Agenda data
    this.syncAirtable()

    // Every 1 second, update agenda if need
    let updateAgenda = setInterval(() => {
      this.checkNext()
    }, 999)

    // Every 15 seconds, sync with Airtable
    let updateData = setInterval(() => {
      this.syncAirtable()
    }, 15000)

  },

  methods:{

    // Update current agenda if nessesary
    checkNext(){
      var i
      for(i=0; i<this.items.length; i++){
        var eventTime = new Date(this.items[i].start)
        if(eventTime > Math.trunc((new Date()).getTime())){
          this.eventNow = this.items[i]
          this.eventNext = this.items[i+1]
          console.log(
            '['+this.parseHMS((new Date()).getTime())+'] ' +
            'now:' + this.eventNow.Name +
            ' next:' + this.eventNext.Name
          );
          return
        }
      }
    },


    // Download agenda data from Airtable
    syncAirtable(){
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
      console.log(
        '['+this.parseHMS((new Date()).getTime())+'] ' +
        'Synced with Airtable'
      )
      return
    },

    // Translate milliseconds into <Hr>:<Min>:<Sec> format
    parseHMS(ms){
      var dat = new Date(ms)
      return twoDigits(dat.getHours()) + ':' +
      twoDigits(dat.getMinutes()) + ':' +
      twoDigits(dat.getSeconds())
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

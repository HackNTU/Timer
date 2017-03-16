<template lang="html">
  <svg>

    <line x1="12" y1="0" x2="12" y2="1080"stroke-width="3" stroke="#95989A"/>
    <line x1="12" y1="180" x2="38" y2="180"stroke-width="2" stroke="#95989A"/>
    <line x1="12" y1="360" x2="38" y2="360"stroke-width="2" stroke="#95989A"/>
    <circle cx="12" cy="180" r="10" stroke="#95989A" stroke-width="3" fill="#62C7FC"/>
    <circle cx="12" cy="360" r="10" stroke="#95989A" stroke-width="3" fill="#62C7FC"/>

    <text x="50" y="186" fill="#95989A" class="time">{{ now.time }}</text>
    <text x="50" y="215" fill="#95989A" class="title">{{ now.title }}</text>
    <text x="50" y="235" fill="#95989A" class="subtitle">{{ now.subtitle }}</text>

    <text x="50" y="366" fill="#95989A" class="time">{{ next.time }}</text>
    <text x="50" y="395" fill="#95989A" class="title">{{ next.title }}</text>
    <text x="50" y="415" fill="#95989A" class="subtitle">{{ next.subtitle }}</text>
    
  </svg>
</template>

<script>
export default {
  name: 'agenda',
  data(){
    return{
      now: {
        time: '10:00 - 11:30',
        title: '主標題TitleABC',
        subtitle:'小標題內容TitleABC'
      },
      next: {
        time: '10:00 - 11:30',
        title: '主標題TitleABC',
        subtitle:'小標題內容TitleABC'
      },
    }
  },
}
</script>

<style lang="css">
/* Blue:   #62C7FC */
/* Green:  #4EF27A */
/* Yellow: #FCFC62 */
/* Pink:   #FC6291 */
svg{
  width: inherit;
  height: inherit;
}

.time{
  font-size: 1.2em;
}
.title{
  font-size: 1.5em;
}
.subtitle{
  font-size: 1em;
}
</style>

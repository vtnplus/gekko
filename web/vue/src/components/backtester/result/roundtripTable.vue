<template lang='jade'>
  .contain.roundtrips
    h2 Roundtrips
    table(v-if='roundtrips.length')
      thead
        tr
          th Entry at
          th Exit at
          th Exposure
          th Entry balance
          th Exit balance
          th P&amp;L
          th Profit
        tr(v-for='rt in roundtrips')
          td {{ fmt(rt.entryAt) }}
          td {{ fmt(rt.exitAt) }}
          td {{ diff(rt.duration) }}
          td {{ round(rt.entryBalance) }}
          td {{ round(rt.exitBalance) }}
          td {{ round(rt.pnl) }}
          td {{ round(rt.profit) }}
    div(v-if='!roundtrips.length')
      p Not enough data to display
</template>

<script>
export default {
  props: ['roundtrips'],
  data: () => {
    return {}
  },
  methods: {
    diff: n => moment.duration(n).humanize(),
    humanizeDuration: (n) => window.humanizeDuration(n),
    fmt: mom => moment.utc(mom).format('YYYY-MM-DD HH:mm'),
    round: n => (+n).toFixed(3),
  },
}
</script>

<style>

.roundtrips {
  margin-top: 50px;
  margin-bottom: 50px;
}

.roundtrips table {
  width: 100%;
}

.roundtrips table th,
.roundtrips table td {
  border: 1px solid #c6cbd1;
  padding: 8px 12px;
}

.roundtrips table tr:nth-child(2n) {
  background-color: #f6f8fa;
}

</style>

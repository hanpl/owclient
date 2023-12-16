<template>
    <div class="footer">
        <p class="date">{{ date  }}</p>
    </div>
    
</template>
<script>
import { format } from 'date-fns'
export default  {
    data() {
      return {
        date: '',
      };
    },
    mounted() {
    setInterval(this.formattedDate, 1000);
    },
    methods: {
      formattedDate() {
      this.date =  format(new Date(), 'dd MMM, yyyy - HH:mm:ss')
    }
    },
    
}
</script>
<style>
.footer {
    background-color: #2c3790;
    left: 0px !important;
    width: 100vw;
    /* height: 43px; */
    position: absolute;
    bottom: 0px;
    padding: 10px;
}
p.date {
    color: white;
    padding-left: 10px;
    font-size: 20px;
    display: contents;
    font-weight: bold;
}
</style>
<template>
  <Title title="Food List Management" />  
  <FormPengeluaran @entri-pengeluaran="entriPengeluaran($event)" />
  <h2>Total Harga : {{ totalPengeluaran }} </h2>
  <ListPengeluaran v-if="showList" :dataPengeluaran="dataPengeluaran" />
</template>

<script>
import Title from './components/Title.vue';
import ListPengeluaran from './components/ListPengeluaran.vue';
import FormPengeluaran from './components/FormPengeluaran.vue';

export default {
  name: 'App',
  components: {
    Title,    
    ListPengeluaran,
    FormPengeluaran
  },
  data(){
    return {
      dataPengeluaran : [
        { nominal: 25000, keterangan : "Ketoprak Spesial"},
        { nominal: 35000, keterangan : "Nasi Ayam Spesial"},
        { nominal: 15000, keterangan : "Soto Ayam"}
      ],
      warning : false,
    }  
  },
  methods:{
    entriPengeluaran(event){
      this.dataPengeluaran.push(event);
    }
  },
  computed: {
    showList: function(){
      return this.dataPengeluaran.length>0; 
    },
    totalPengeluaran: function(){
      return this.dataPengeluaran.reduce((accum, item) => accum+parseInt(item.nominal), 0);
    }
  },
  watch: {
    totalPengeluaran: function(val)
    {
      if(val>100000)
      {
        this.warning = true;
      }
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #000000;
}
</style>

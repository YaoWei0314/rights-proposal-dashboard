<template>
    <div :id="id"></div>
</template>

<script>
import { isProxy, toRaw } from 'vue';

export default {
    name: 'ring-chart',
    props: {
      'data':{
        type: Array
      },
      'id': {
        type: String,
        default: 'main'
      },
      'title': {
        type: String,
        default: '提案類型統計'
      },
      'colors': {
        type: Array,
        default: ['#0a53a8','#215a6c','#e6e6e6','#e7e7e7','#e8eaed']
      },
      'labelFormat': {
        type: String,
        default: '{c}'
      }
    },
	watch:{
		data: {
			handler(val, oldVal){
				this.updateChart();
			},
			deep: true
		}
	},
    methods: {
      updateChart(){
        var myChart = echarts.init(document.getElementById(this.id));
        let rawData = toRaw(this.data);
        let option = {
          title: {
            text: this.title,
            left: 'center',
            top: 'center',
			textStyle: {fontSize: 24}
          },
          series: [
            {
              type: 'pie',
              color: this.colors,
              data: rawData,
              radius: ['60%', '70%'],
              label: {formatter: `{b}: ${this.labelFormat}`,fontSize: 16},
			  colorBy: 'data',
            }
          ],
		  legend: {
			show: true,
			top: 'bottom'
		  }
        };
        myChart.setOption(option);
		
      }
    },
    mounted() {
        this.updateChart();
    }
}

</script>

/*

B5B5B6

FFF362

E1893F

6DA1C8

73B284

DD776A

 */

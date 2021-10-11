<script>
import { Bar } from "vue-chartjs";

export default {
    extends: Bar,
    props:{
        label:{
            type: String
        },
        chartData:{
            type: Array
        },
        options:{
            type: Object,
        }
    },
    mounted(){
        var daydecideCnt= []
        const dates = this.chartData.map(d=>d.stateDt).reverse();
        const totals = this.chartData.map(d=>d.total);

        dates.shift()
        
        for(var i=0; i<8; i++){
            daydecideCnt.push(totals[i]-totals[i+1])
        }
        const daystate = daydecideCnt.reverse()
    
        

        this.renderChart({
            labels: dates,
            datasets: [
                {
                label: this.label,
                data: daystate,
                barThickness: 12,
                
                backgroundColor: 'rgba(75,137,220,0.9)',
                hoverBackgroundColor: 'rgba(75,137,220)'

            }
            ]
        },
            this.options
        );
    }
};
</script>

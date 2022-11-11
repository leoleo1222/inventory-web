<template>
    <div>
        <apexchart width="580" type="donut" :options="options" :series="series"></apexchart>
    </div>
</template>

<script>
// @ is an alias to /src
import { ref, onMounted } from "vue";

export default {
    name: 'ChartView',
    components: {

    },
    setup() {
        const options = ref({});
        const series = ref([]);
        onMounted(async () => {

            var response = await fetch("/api/bookings/aggregate/groupby");

            if (response.ok) {
                var heroes = await response.json();

                series.value = heroes.map(a => a.count);
                options.value = { labels: heroes.map(a => a._id) };
            }
        });
        return {
            options, series
        }
    }
}
</script>

<script>
import { Line } from 'vue-chartjs';

export default {
  extends: Line,
  props: ['labels', 'data', 'options'],
  methods: {
    renderLineChart: function() {
      this.renderChart({ labels: this.labels, datasets: this.data }, this.options);
    }
  },
  mounted() {
    this.renderLineChart();
  }
};
</script>

<style></style>

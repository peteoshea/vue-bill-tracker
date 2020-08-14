<script>
import { Bar } from "vue-chartjs";
import moment from "moment";

const last12Months = () => {
  const months = [
    "January",
    "February",
    "March",
    "April",
    "May",
    "June",
    "July",
    "August",
    "September",
    "October",
    "November",
    "December",
  ];

  const today = new Date();
  const orderedMonths = [];
  let month = today.getMonth() + 1;

  // Correctly handle december
  if (month === 12) {
    month = 0;
  }

  for (let i = 0; i < 12; i++) {
    orderedMonths.push(months[month]);
    month === 11 ? (month = 0) : month++;
  }

  return orderedMonths;
};

const processBills = (bills) => {
  const oneYearAgo = moment().subtract(1, "years");
  const months = last12Months();
  const monthValues = new Array(12).fill(0);

  for (const bill of bills) {
    if (moment(bill.date).isSameOrBefore(oneYearAgo)) {
      continue;
    }
    const monthName = moment(bill.date).format("MMMM");
    const indexOfMonth = months.indexOf(monthName);
    monthValues[indexOfMonth] += parseInt(bill.amount);
  }

  return monthValues;
};

export default {
  extends: Bar,
  name: "Chart",
  props: ["bills"],
  methods: {
    displayChart() {
      this.renderChart({
        labels: last12Months(),
        datasets: [
          {
            label: "Amount",
            backgroundColor: "lightblue",
            data: processBills(this.bills),
          },
        ],
      });
    },
  },
  mounted() {
    this.displayChart();
  },
  watch: {
    bills() {
      this.displayChart();
    }
  }
};
</script>

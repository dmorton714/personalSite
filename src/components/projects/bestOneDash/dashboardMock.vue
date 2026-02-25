<script setup>
import { ref, onMounted } from 'vue'
import Chart from 'chart.js/auto'

// Menu Toggle State
const isMenuActive = ref(false)
const toggleMenu = () => {
  isMenuActive.value = !isMenuActive.value
}

// Chart Refs
const pieChartRef = ref(null)
const barChartRef = ref(null)

// Mock Data based on CSV context
const mockInvoices = ref([
  { date: '2023-04-21', type: 'INVC', ref: '3700006923', customer: 'SOUTHERN INDIANA SCALE CO', qty: 1, price: 45 },
  { date: '2023-04-14', type: 'INVC', ref: '3700006854', customer: 'MILLERS AUTO BODY', qty: 1, price: 45 },
  { date: '2023-03-14', type: 'INVC', ref: '3700006520', customer: 'RIVER METALS REC LOU STL', qty: 4, price: 39 },
  { date: '2023-02-20', type: 'INVC', ref: '3700006284', customer: 'ROGERS GROUP (KY)', qty: 3, price: 42 },
  { date: '2023-02-17', type: 'VINV', ref: '13720', customer: 'VOID', qty: 4, price: 39 },
  { date: '2023-02-10', type: 'INVC', ref: '3700006212', customer: 'RIVER METALS REC - NEWPOR', qty: 4, price: 40.5 },
  { date: '2023-01-16', type: 'INVC', ref: '3700005942', customer: 'LEHIGH HANSON-CEMENT', qty: 1, price: 45 },
  { date: '2023-01-05', type: 'INVC', ref: '3700005882', customer: 'HILLTOP BIG BEND QUARRY', qty: 2, price: 42 }
])

const mockTasks = ref([
  { title: 'Follow up on Void', subtitle: 'Ref: 13720' },
  { title: 'Re-bill ROGERS GROUP', subtitle: 'Ref: 3700006284' },
  { title: 'Month-end reconciliation', subtitle: 'Due: 05/01/2023' },
  { title: 'Follow up on Void', subtitle: 'Ref: 13720' },
  { title: 'Re-bill ROGERS GROUP', subtitle: 'Ref: 3700006284' },
  { title: 'Month-end reconciliation', subtitle: 'Due: 05/01/2023' }
])

// Chart Initialization
onMounted(() => {
  const blue = '#3d92bf'
  const red = '#e7004f'
  const yellow = '#ffd966'
  const grey = '#e0e1e9'
  const black = '#000000'
  const black2 = '#999'

  // Pie Chart
  if (pieChartRef.value) {
    new Chart(pieChartRef.value, {
      type: 'pie',
      data: {
        labels: ['Completed', 'Voided', 'Pending'],
        datasets: [{
          label: 'Invoice Status',
          data: [8, 1, 1],
          backgroundColor: [blue, red, yellow],
        }]
      },
      options: {
        responsive: true,
        animation: { duration: 2000 },
        plugins: {
          title: { display: true, text: 'Invoice Status', font: { size: 18 }, padding: { top: 5, bottom: 15 } }
        }
      }
    })
  }

  // Bar Chart
  if (barChartRef.value) {
    new Chart(barChartRef.value, {
      type: 'bar',
      data: {
        labels: ["January", "February", "March", "April"],
        datasets: [{
          label: 'Net Profit',
          data: [129, 249, 156, 90],
          backgroundColor: [red, yellow],
        }]
      },
      options: {
        responsive: true,
        animation: { duration: 2000 },
        plugins: {
          legend: { display: false },
          title: { display: true, text: 'Monthly Gross Profit', font: { size: 18 }, padding: { top: 5, bottom: 15 } }
        }
      }
    })
  }
})
</script>

<template>
  <div class="dashboard-wrapper">
    <div :class="['navigation', { active: isMenuActive }]">
      <ul>
        <li>
          <a href="#" @click.prevent>
            <span class="logo">
              <img src="/bestone/tirebuddy.png" alt="Tire Buddy" style="max-width: 68px; max-height: 68px;">
            </span>
          </a>
        </li>
        <li>
          <a href="#" @click.prevent>
            <span class="icon"><img src="/svg/speedometer-outline.svg" alt="Home"></span>
            <span class="title">Home</span>
          </a>
        </li>
        <li>
          <a href="#" @click.prevent>
            <span class="icon"><img src="/svg/mail-outline.svg" alt="Reports"></span>
            <span class="title">Reports</span>
          </a>
        </li>
        <li>
          <a href="#" @click.prevent>
            <span class="icon"><img src="/svg/people-outline.svg" alt="Customers"></span>
            <span class="title">Customers</span>
          </a>
        </li>
        <li>
          <a href="#" @click.prevent>
            <span class="icon"><img src="/svg/newspaper-outline.svg" alt="Invoices"></span>
            <span class="title">Invoices</span>
          </a>
        </li>
      </ul>
    </div>

    <div :class="['main', { active: isMenuActive }]">
      <div class="topbar">
        <div class="toggle" @click="toggleMenu">
          <img src="/svg/menu-outline.svg" style="max-width: 28px; max-height: 28px;" alt="Menu">
        </div>

        <div class="search">
          <label>
            <input type="text" placeholder="Search invoices...">
            <img src="/svg/search-outline.svg" style="max-width: 28px; max-height: 28px;" alt="Search">
          </label>
        </div>

      </div>

      <div class="cardBox">
        <div class="card">
          <div>
            <div class="numbers">$8,240</div>
            <div class="cardName">Gross Total</div>
          </div>
          <div class="iconBox"><img src="/svg/cash-outline.svg" alt="Gross"></div>
        </div>
        <div class="card">
          <div>
            <div class="numbers">10</div>
            <div class="cardName">Total Invoices</div>
          </div>
          <div class="iconBox"><img src="/svg/newspaper-outline.svg" alt="Invoices"></div>
        </div>
        <div class="card">
          <div>
            <div class="numbers">$6,850</div>
            <div class="cardName">Net Profit</div>
          </div>
          <div class="iconBox"><img src="/svg/cash-outline.svg" alt="Net"></div>
        </div>
        <div class="card">
          <div>
            <div class="numbers">1</div>
            <div class="cardName">Voided</div>
          </div>
          <div class="iconBox"><img src="/svg/alert-outline.svg" alt="Alerts"></div>
        </div>
      </div>

      <div class="graphBox">
        <div class="box">
          <canvas ref="pieChartRef"></canvas>
        </div>
        <div class="box">
          <canvas ref="barChartRef"></canvas>
        </div>
      </div>

      <div class="details">
        <div class="workOrders">
          <div class="cardHeader">
            <h2>Recent Invoices</h2>
            <a href="#" @click.prevent class="btn">View All</a>
          </div>
          <table>
            <thead>
              <tr>
                <td>Date</td>
                <td>Ref #</td>
                <td>Customer</td>
                <td>Amount</td>
                <td>Status</td>
              </tr>
            </thead>
            <tbody>
              <tr v-for="(invoice, index) in mockInvoices" :key="index">
                <td>{{ invoice.date }}</td>
                <td>{{ invoice.ref }}</td>
                <td>{{ invoice.customer }}</td>
                <td>${{ (invoice.qty * invoice.price).toFixed(2) }}</td>
                <td>
                  <span :class="['status', invoice.type === 'INVC' ? 'Completed' : 'pending']">
                    {{ invoice.type === 'INVC' ? 'Completed' : 'Voided' }}
                  </span>
                </td>
              </tr>
            </tbody>
          </table>
        </div>

        <div class="recentCustomers">
          <div class="cardHeader">
            <h2>Action Items</h2>
            <a href="#" @click.prevent class="btn">View All</a>
          </div>
          <table>
            <tr v-for="(task, index) in mockTasks" :key="index">
              <td width="60">
                <div class="imgBx">
                  <img src="https://cdn.outsideonline.com/wp-content/uploads/2023/03/Funny_Dog_H.jpg?crop=16:9&width=960&enable=upscale&quality=100" alt="Task">
                </div>
              </td>
              <td>
                <h4>{{ task.title }}<br><span>{{ task.subtitle }}</span></h4>
              </td>
            </tr>
          </table>
        </div>
      </div>
    </div>
  </div>
</template>



<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Roboto:wght@400;500;700&display=swap');

* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
    font-family: sans-serif;
}

.dashboard-wrapper {
    --blue: #3d92bf;
    --red: #e7004b;
    --white: #fff;
    --grey: #e0e1e9;
    --black: #000000;
    --black2: #999;
    --yellow: #ffd966;
    display: flex; 
    position: relative;
    width: 100%;
    min-height: 800px;
    background: var(--grey);
    border-radius: 10px;
    overflow: hidden;
    box-shadow: 0 10px 40px rgba(0,0,0,0.15);
}

/* --- NAVIGATION --- */
.navigation {
  position: relative;
  width: 200px;
  flex-shrink: 0;
  background: var(--black);
  transition: 0.5s;
  overflow: hidden;
  z-index: 10;
}

.navigation.active {
  width: 70px;
}

.navigation ul {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
}

.navigation ul li {
  position: relative;
  width: 100%;
  list-style: none;
  border-top-left-radius: 20px;
  border-bottom-left-radius: 20px;
}

.navigation ul li:hover,
.navigation ul li.hovered {
  background: var(--grey);
}

.navigation ul li:nth-child(1) {
  margin-bottom: 50px;
  pointer-events: none;
}

.navigation ul li a {
  position: relative;
  display: flex;
  width: 100%;
  text-decoration: none;
  color: var(--white);
}

.navigation ul li:hover a,
.navigation ul li.hovered a {
  color: var(--blue);
}

.logo {
  display: flex;
  justify-content: center;
  align-items: center;
  width: 70px;
  height: 90px;
  padding-top: 20px;
}

.navigation.active .title { display: none; }
.navigation.active li:first-child .title { display: inline; }
.navigation.active ul li a .title { display: block; }
.navigation.active .logo { width: 70px; }

.icon img {
  filter: brightness(0) invert(1);
  max-width: 28px;
  max-height: 28px;
}

.navigation ul li a .icon {
  position: relative;
  display: flex;
  justify-content: center;
  align-items: center;
  min-width: 60px;
  height: 60px;
  text-align: center;
  line-height: 60px;
  font-size: 1.75em;
}

.navigation ul li a .title {
  position: relative;
  display: block;
  padding: 0 10px;
  line-height: 60px;
  text-align: start;
  white-space: nowrap;
}

/* curve outside */
.navigation ul li:hover a::before,
.navigation ul li.hovered a::before {
  content: '';
  position: absolute;
  right: 0;
  top: -50px;
  width: 50px;
  height: 50px;
  background: transparent;
  border-radius: 50%;
  box-shadow: 35px 35px 0 10px var(--grey);
  pointer-events: none;
}

.navigation ul li:hover a::after,
.navigation ul li.hovered a::after {
  content: '';
  position: absolute;
  right: 0;
  bottom: -50px;
  width: 50px;
  height: 50px;
  background: transparent;
  border-radius: 50%;
  box-shadow: 35px -35px 0 10px var(--grey);
  pointer-events: none;
}

/* --- MAIN CONTENT --- */
.main {
  position: relative;
  flex-grow: 1;
  background: var(--grey);
  transition: 0.5s;
  overflow-y: auto; 
}

.topbar {
  width: 100%;
  height: 60px;
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 0 10px;
}

.toggle {
  position: relative;
  width: 60px;
  height: 60px;
  display: flex;
  justify-content: center;
  align-items: center;
  font-size: 2.5em;
  cursor: pointer;
}

.search {
  position: relative;
  width: 400px;
  margin: 0 10px;
}

.search label { position: relative; width: 100%; }

.search label input {
  width: 100%;
  height: 40px;
  border-radius: 40px;
  padding: 5px 20px 5px 35px;
  font-size: 18px;
  outline: none;
  border: 1px solid var(--black2);
}

.search label img {
  position: absolute;
  top: -5px; 
  left: 8px;
  font-size: 1.2em;
}

.user {
  position: relative;
  width: 40px;
  height: 40px;
  border-radius: 50%;
  overflow: hidden;
  cursor: pointer;
}

.user img {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  object-fit: cover;
}

/* cards 4 boxes up top */
.cardBox {
  position: relative;
  width: 100%;
  padding: 10px;
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-gap: 10px;
}

.cardBox .card {
  position: relative;
  background-color: var(--white);
  padding: 30px;
  border-radius: 20px;
  display: flex;
  justify-content: space-between;
  cursor: pointer;
  box-shadow: 0 7px 25px rgba(0,0,0,0.08);
}

.cardBox .card .numbers {
  position: relative;
  font-weight: 500;
  font-size: 2.5em;
  color: var(--blue);
}

.cardBox .card .cardName {
  color: var(--black2);
  font-size: 1.1em;
  margin-top: 5px;
}

.cardBox .card .iconBox img {
  font-size: 3.5em;
  color: var(--black2);
  margin-left: 10px;
  max-width: 40px;
  max-height: 40px;
  fill: brightness(0) invert(1);
}

.cardBox .card:hover { background-color: var(--blue); }
.cardBox .card:hover .numbers,
.cardBox .card:hover .cardName,
.cardBox .card:hover .iconBox { color: var(--white); }

/* charts */
.graphBox {
  position: relative;
  width: 100%;
  padding: 10px;
  display: grid;
  grid-template-columns: 1fr 2fr;
  grid-gap: 10px;
  min-height: 150px;
}

.graphBox .box {
  position: relative;
  background-color: var(--white);
  padding: 10px;
  width: 100%;
  box-shadow: 0 7px 25px rgba(0,0,0,0.08);
  border-radius: 20px;
}

canvas { max-width: 100%; max-height: 100%; display: block; }

/* work orders */
.details {
  position: relative;
  width: 100%;
  padding: 10px;
  display: grid;
  grid-template-columns: 2fr 1fr;
  grid-gap: 10px;
}

.details .workOrders {
  position: relative;
  display: grid;
  min-height: 500px;
  background-color: var(--white);
  padding: 10px;
  border-radius: 20px;
  box-shadow: 0 7px 25px rgba(0,0,0,0.08);
}

.cardHeader {
  display: flex;
  justify-content: space-between;
  align-items: flex-start;
}

.cardHeader h2 {
  font-weight: 600;
  color: var(--blue);
}

.btn {
  position: relative;
  padding: 5px 10px;
  background-color: var(--blue);
  text-decoration: none;
  color: var(--white);
  border-radius: 6px;
}

.details table {
  width: 100%;
  border-collapse: collapse;
  margin-top: 10px;
}

.details table thead td { font-weight: 600; }

.details .workOrders table tr {
  border-bottom: 1px solid var(--black2);
}

.details .workOrders table tr:last-child { border-bottom: none; }
.details .workOrders table tbody tr:hover { background-color: var(--blue); color: var(--white); }
.details .workOrders table tr td { padding: 10px; }
.details .workOrders table tr td:last-child { text-align: end; }
.details .workOrders table tr td:nth-child(2) { text-align: end; }
.details .workOrders table tr td:nth-child(3) { text-align: center; }

.status {
  padding: 2px 4px;
  border-radius: 4px;
  font-size: 14px;
  font-weight: 500;
  color: var(--white);
}
.status.Completed { background: #8de02c; }
.status.pending { background: #e7004b; }
.status.inprocess { background: #ffd966; }

.recentCustomers {
  position: relative;
  display: grid;
  min-height: 500px;
  padding: 10px;
  background: var(--white);
  box-shadow: 0 7px 25px rgba(0,0,0,0.08);
  border-radius: 20px;
}

.recentCustomers .imgBx {
  position: relative;
  width: 40px;
  height: 40px;
  border-radius: 50%;
  overflow: hidden;
}

.recentCustomers .imgBx img {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  object-fit: cover;
}

.recentCustomers table tr td { padding: 12px 10px; }
.recentCustomers table tr td h4 { font-size: 16px; font-weight: 500; line-height: 1.2em; }
.recentCustomers table tr td h4 span { font-size: 14px; color: var(--black2); }
.recentCustomers table tr:hover { background-color: var(--blue); color: var(--white); }
.recentCustomers table tr:hover td h4 span { color: var(--white); }

/* responsive tweaks for the embed */
@media (max-width: 991px) {
  .graphBox { grid-template-columns: 1fr; height: auto; }
  .cardBox { grid-template-columns: repeat(2, 1fr); }
  .details { grid-template-columns: 1fr; }
}
@media (max-width: 768px) {
  .navigation { width: 70px; }
  .navigation .title { display: none; }
}
</style>
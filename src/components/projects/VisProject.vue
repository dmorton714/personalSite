<script setup>
import { ref, onMounted, onUnmounted } from "vue";
import ImageStack from "./ImageStack.vue";
import Dashboardmock from "./bestOneDash/dashboardMock.vue";

const scrollProgress = ref(0);
const pathLength = 5414.29;

const handleScroll = () => {
  const section = document.getElementById("scroll-section");
  if (!section) return;

  const rect = section.getBoundingClientRect();
  const windowHeight = window.innerHeight;

  const total = rect.height + windowHeight;
  const progress = (windowHeight - rect.top) / total;

  scrollProgress.value = Math.min(Math.max(progress, 0), 1);
};

onMounted(() => {
  window.addEventListener("scroll", handleScroll);
  handleScroll();

  const elements = document.querySelectorAll(".box, img");

  const observer = new IntersectionObserver(
    (entries) => {
      entries.forEach((entry) => {
        if (entry.isIntersecting) {
          entry.target.classList.add("visible");
        }
      });
    },
    { threshold: 0.2 },
  );

  elements.forEach((el) => observer.observe(el));
});

onUnmounted(() => {
  window.removeEventListener("scroll", handleScroll);
});
</script>

<template>
  <header class="page-header">
    <h1>The Problem</h1>

    <p>
      We needed to analyze sales performance for a single product across
      multiple retail locations using exports from a legacy Point of Sale (POS)
      system.
    </p>

    <p>The core objectives were:</p>

    <ul>
      <li>Identify top customers by revenue and volume</li>
      <li>Rank store performance</li>
      <li>Calculate units sold per location</li>
      <li>Detect inconsistencies across reports</li>
      <li>Consolidate fragmented data into a reliable, structured dataset</li>
    </ul>

    <p>
      The primary challenge was not analytics — it was data acquisition and
      normalization. Reports were manually generated, inconsistently formatted,
      and separated across multiple sheets and stores.
    </p>

    <p>
      To produce meaningful insights, we first needed to build a repeatable data
      pipeline.
    </p>
    <img src="/bestone/tirebuddy.png" alt="Tire Buddy Logo" class="header-bg-logo" />
  </header>

  <section id="scroll-section">
    <svg
      class="line-svg"
      preserveAspectRatio="xMidYMin slice"
      width="100%"
      fill="none"
      viewBox="-480 0 2300 2241"
    >
      <path
        stroke="#000000"
        stroke-width="160"
        :stroke-dasharray="pathLength"
        :stroke-dashoffset="
          pathLength - pathLength * Math.min(scrollProgress * 1.4, 1)
        "
        d="M-841 100H584c124 0 225 101 225 225v0c0 124-101 225-225 225h-95a281 281 0 00-281 281v0c0 155 125 281 281 281h442c167 0 304 136 304 304v0c0 168-137 304-304 304H795a439 439 0 00-439 439v82"
        opacity=".45"
      />
    </svg>

    <div class="container">
      <h2>Vis Reporting</h2>

      <div class="layout-container">
        <div class="box box-1">
          <h3>Automated Data Extraction</h3>
          <p>
            The POS system did not provide an API, so I implemented a
            Selenium-based browser automation workflow to programmatically
            retrieve reports.
          </p>

          <p>The automation handled the following tasks:</p>

          <ul>
            <li>Authenticated into the POS web interface</li>
            <li>Navigated dynamic reporting views</li>
            <li>Triggered report generation</li>
            <li>Downloaded and organized exported files</li>
            <li>
              Standardized file naming conventions for downstream processing
            </li>
          </ul>

          <p>
            This replaced a manual, multi-step workflow and reduced report
            collection time from hours to minutes. (Automation component removed
            from public demo due to sensitive credentials.)
          </p>

          <p>
            <strong>Key takeaway:</strong> When APIs don’t exist, automation
            becomes infrastructure.
          </p>
        </div>

        <div class="image-1">
          <ImageStack />
        </div>

        <div class="box box-2">
          <h3>Data Cleaning & Normalization</h3>
          <p>
            Each exported report contained structural inconsistencies,
            including:
          </p>

          <ul>
            <li>Redundant headers</li>
            <li>Irrelevant columns</li>
            <li>Store-specific formatting differences</li>
            <li>Mixed Customers and product labeling</li>
            <li>Inconsistent information across sheets</li>
          </ul>

          <br />
          <p>Using Python (pandas), I built a cleaning pipeline that:</p>

          <ul>
            <li>Dropped non-essential columns</li>
            <li>Standardized schema across all stores</li>
            <li>Normalized date formats and numeric types</li>
            <li>Cleaned currency fields and unit counts</li>
            <li>Unified naming conventions</li>
            <li>
              Merged seven independent sheets into a single master dataset
            </li>
          </ul>

          <p>
            The output was a normalized, analysis-ready dataframe with
            consistent structure across all locations. This stage transformed
            raw exports into a reliable source of truth.
          </p>
        </div>

        <img
          class="image-2"
          src="/bestone/cleaning.png"
        />

        <div class="box box-3">
          <h3>Analytical Layer & Reusable Metrics</h3>
          <p>
            With structured data in place, I implemented modular functions to
            compute key performance metrics:
          </p>

          <ul>
            <li>Top customers by revenue</li>
            <li>Top customers by units purchased</li>
            <li>Revenue per store</li>
            <li>Units sold per store</li>
            <li>Distribution and ranking analysis</li>
            <li>Time-based aggregation</li>
          </ul>

          <p>
            Functions were written to be reusable and parameterized, allowing
            flexible filtering by store, date range, or customer. This reduced
            analysis from manual spreadsheet inspection to deterministic,
            reproducible computations.
          </p>

          <p>
            The result: scalable insight generation rather than one-off
            reporting.
          </p>
        </div>

        <img
          class="image-3"
          src="/bestone/all_stores_gnp.jpg"
        />

        <div class="box box-4">
          <h3>Interactive Dashboard & Visualization</h3>
          <p>
            To surface insights for non-technical stakeholders, I built an
            interactive dashboard layer.
          </p>

          <p>The dashboard enabled the following capabilities:</p>
          <ul>
            <li>Displays ranked store performance</li>
            <li>Highlights high-value customers</li>
            <li>Allows filtering and sorting</li>
            <li>Visualizes sales distribution across locations</li>
            <li>Presents clean, decision-ready metrics</li>
          </ul>

          <p>This allowed management to:</p>
          <ul>
            <li>Identify top-performing stores immediately</li>
            <li>Detect underperformance</li>
            <li>Adjust inventory strategy</li>
            <li>Recognize customer purchasing patterns</li>
          </ul>

          <p>
            The project shifted reporting from reactive spreadsheet review to
            proactive, data-driven decision support.
          </p>
        </div>

        <img
          class="image-4"
          src="/bestone/visdash.jpg"
        />


        <div class="box box-3">
          <h3>Engineering Impact</h3>
          <p>This project demonstrates:</p>
          <ul>
            <li>Automation in environments without APIs</li>
            <li>Practical data engineering and normalization</li>
            <li>Analytical modeling using structured data</li>
            <li>
              Clear separation between data pipeline and presentation layer
            </li>
            <li>Building internal tooling to improve operational visibility</li>
          </ul>
          <p>
            It began as a reporting problem. It became a lightweight data
            pipeline with a decision-support interface.
          </p>
          <a href="#" class="btn">Find out more</a>
        </div>
      </div>
    </div>
  </section>

  <div class="dashboard-preview-wrapper">
    <Dashboardmock />
  </div>

  <section class="bottom"></section>
</template>

<style scoped>
body {
  margin: 0;
  font-family: "Montserrat", sans-serif;
  width: 100%;
}

.page-header {
  position: relative;
  display: block;
  width: 100%;
  margin: 0 auto;
  padding: 6rem 2rem;
  line-height: 1;
  background: linear-gradient(135deg, #B32522 0%, #721816 100%);
  color: white;
}

.header-bg-logo {
  position: absolute;
  bottom: 2rem;
  right: 2rem;
  height: 550px;
  width: auto;
  opacity: 0.15 !important;
  pointer-events: none;
  z-index: 1;
}

.page-header > * {
  max-width: 900px;
}

.page-header h1 {
  font-size: clamp(3rem, 6vw, 5rem);
  font-weight: 800;
  letter-spacing: -0.02em;
  margin-bottom: 2rem;
  line-height: 1.1;
}

.page-header p {
  font-size: 1.2rem;
  line-height: 1.7;
  color: rgba(255, 255, 255, 0.9);
  margin-bottom: 1.5rem;
}

.page-header ul {
  margin: 2rem 0;
  padding-left: 1.5rem;
}

.page-header li {
  font-size: 1.15rem;
  margin-bottom: 0.75rem;
  line-height: 1.6;
  position: relative;
}

.page-header li::marker {
  color: #a5c8ff;
}

#scroll-section {
  position: relative;
  min-height: 2700px;
  display: grid;
}

.line-svg {
  grid-row: 1;
  grid-column: 1;
  height: 100%;
  min-width: 300px;
  z-index: 1;
}

.container {
  grid-column: 1;
  grid-row: 1;
  margin: 0 auto;
  width: 100%;
  padding: 0 4rem;
  z-index: 2;
}

h2 {
  color: rgb(0, 0, 0);
  font-size: 62px;
  font-weight: 900;
  text-align: right;
  padding-top: 72px;
}

.layout-container {
  padding-top: 8rem;
  display: grid;
  grid-template-columns: repeat(6, 1fr);
  gap: 2rem;
}

.box {
  background: white;
  padding: 4rem;
  transform: scale(0.8);
  opacity: 0;
  transition: all 0.6s ease;
  box-shadow: 0 30px 50px rgba(0, 0, 0, 0.425);
}

.box.visible {
  transform: scale(1);
  opacity: 1;
}

.box h3 {
  font-size: 32px;
  margin-bottom: 1rem;
}

.box p {
  font-size: 16px;
  margin-bottom: 1.5rem;
}

img {
  width: 100%;
  opacity: 0;
  transform: scale(0.8);
  transition: all 0.6s ease;
}

img.visible {
  opacity: 1;
  transform: scale(1);
}

.btn {
  background: rgb(32, 91, 173);
  color: white;
  padding: 10px 30px;
  border-radius: 999px;
  text-decoration: none;
  font-weight: bold;
  display: inline-block;
  transition: 0.3s;
}

.btn:hover {
  background: rgb(222, 40, 112);
}

/* Layout positions */
.box-1 {
  grid-column: 3 / span 3;
}

.image-1 {
  grid-column: 1 / span 2;
}

.box-2 {
  grid-column: 2 / span 3;
  position: relative;
  z-index: 2;
}

.image-2 {
  grid-column: 5 / span 3;
  width: 400px;
  margin-left: -120px;
  margin-top: 60px; 
  z-index: 1; 
  transform: scale(0.8) rotate(12deg); 
}

img.image-2.visible {
  opacity: 1;
  transform: scale(1.1) rotate(12deg);
}

.box-3 {
  grid-column: 3 / span 3;
  position: relative;
  z-index: 2;
}

.image-3 {
  grid-column: 2 / span 2;
  width: 600px;
  margin-left: -120px;
  margin-top: -320px; 
  z-index: 1;
  transform: scale(0.8) rotate(20deg); 
}

img.image-3.visible {
  opacity: 1;
  transform: scale(1.1) rotate(20deg);
}

.box-4 {
  grid-column: 1 / span 3;
  z-index: 2;
}

.image-4 {
  grid-column: 4 / span 2;
  width: 600px;
  margin-left: -20px;
  margin-top: 60px; 
  z-index: 1;
  transform: scale(0.8) rotate(10deg); 
}

img.image-4.visible {
  opacity: 1;
  transform: scale(1.1) rotate(10deg);
}

.dashboard-preview-wrapper {
  position: relative;
  width: 100%;
  height: auto; 
  margin: 4rem auto;
  overflow: hidden;
  box-shadow: 0 20px 50px rgba(0,0,0,0.3);
}

.bottom {
  height: 10vh;
}
</style>

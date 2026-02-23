<script setup>
import { ref, onMounted, onUnmounted } from "vue";

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
      The non-profit organization <strong>Code:You</strong> faced a major hurdle in student placement: job
      opportunities were scattered across multiple Slack channels, leading to "link rot" and invisible data. Fresh
      bootcamp graduates struggled to find relevant roles, and the staff had no way to track which skills were actually
      in demand.
    </p>

    <p>The core challenges addressed in this project were:</p>
    <ul>
      <li><strong>Lack of Centralization:</strong> Important job leads were lost in fast-moving chat histories.</li>
      <li><strong>Data Expiration:</strong> No system existed to prune dead links, leading to a poor user experience for
        job seekers</li>
      <li><strong>Visibility Gaps:</strong> Leadership had no metrics on salary trends, regional demand, or required
        tech stacks</li>
      <li><strong>Junior Skill Gaps:</strong> Coordinating 9 junior developers required a technical roadmap that
        balanced learning with production-grade delivery</li>
    </ul>
    <p> <strong>Key takeaway:</strong> We didn't just build a website; we built a <strong>labor market intelligence
        tool</strong> that allowed students to identify and fill their own skill gaps based on real-time data </p>

  </header>

  <section id="scroll-section">
    <svg class="line-svg" preserveAspectRatio="xMidYMin slice" width="100%" fill="none" viewBox="-480 0 2300 2241">
      <path stroke="#022f47" stroke-width="160" :stroke-dasharray="pathLength" :stroke-dashoffset="pathLength - pathLength * Math.min(scrollProgress * 1.4, 1)
        "
        d="M-841 100H584c124 0 225 101 225 225v0c0 124-101 225-225 225h-95a281 281 0 00-281 281v0c0 155 125 281 281 281h442c167 0 304 136 304 304v0c0 168-137 304-304 304H795a439 439 0 00-439 439v82"
        opacity=".45" />
    </svg>

    <div class="container">
      <h2>Code:You: From Slack to Web</h2>

      <div class="layout-container">
        <div class="box box-1">
          <h3>Project Roadmap:</h3>
          <p>
            As Project Manager and Technical Advisor, I led the team through a five-stage deployment to move from manual
            messaging to an automated, data-driven platform.
          </p>
          <ul>
            <li> <strong>1. Internal Ingestion & Validation:</strong> We developed a standardized staff input form to
              replace unstructured Slack posts. This ensured every job entry contained critical metadata like salary,
              region, and required languages. </li>
            <li> <strong>2. Redundant Data Architecture:</strong> We designed a hybrid storage solution using
              <strong>MongoDB</strong> for high-performance querying, with a <strong>Google Sheets failover</strong>.
              This provided the non-profit staff with a familiar interface for manual audits while maintaining a
              professional database backend.
            </li>
            <li> <strong>3. Automated Lifecycle Management:</strong> To solve the "dead link" problem, we implemented a
              30-day expiration logic. Posts were automatically flagged or archived after 30 days, ensuring students
              only spent time on active opportunities. </li>
            <li> <strong>4. Analytical Dashboarding:</strong> We built a decision-support interface that aggregated job
              data. This allowed students to visualize demand by region (State vs. Remote) and identify the most
              requested languages/skills in the current market. </li>
            <li> <strong>5. Technical Mentorship & Code Review:</strong> Beyond the architecture, I managed the
              9-developer sprint cycle, stepping in to resolve blockers in database schema design and UI/UX consistency
              to ensure the final product was production-ready. </li>
          </ul>
          <a href="#" class="btn">Find out more</a>
        </div>

        <img class="image-1" src="https://assets.codepen.io/732/matthew-deltoro-LdFvvpjnB2A-unsplash-800.jpg" />

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
            <li>Mixed date and currency formats</li>
            <li>Inconsistent product labeling</li>
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
          <a href="#" class="btn">Find out more</a>
        </div>

        <img class="image-2" src="https://assets.codepen.io/732/viviana-rishe-6fNZ7QtXiCs-unsplash-800.jpg" />

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
          <a href="#" class="btn">Find out more</a>
        </div>

        <img class="image-3" src="https://assets.codepen.io/732/colton-sturgeon-FiCPutl_aog-unsplash-800.jpg" />

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
          <a href="#" class="btn">Find out more</a>
        </div>

        <div class="box box-3">
          <h3>Engineering Impact</h3>
          
          <p>This project demonstrates:</p>
          <ul>
            <li><strong>Strategic Project Management:</strong> Leading a large team of junior developers through a
              complex SDLC.</li>
            <li><strong>Fault-Tolerant System Design:</strong> Implementing database failovers to ensure 100% uptime for
              non-profit operations.</li>
            <li><strong>Automation in environments without APIs:</strong> Bridging the gap between manual staff input
              and automated public displays.</li>
            <li><strong>Decision-Support Engineering:</strong> Turning raw job posts into actionable insights for
              student career pivots.</li>
            <li><strong>Building internal tooling to improve operational visibility:</strong> Providing leadership with
              the first-ever clear view of their graduates' hiring landscape.</li>
          </ul>

          <p>
            It began as a reporting problem. It became a lightweight data pipeline with a decision-support interface.
          </p>
          <a href="#" class="btn">Find out more</a>
        </div>
      </div>
    </div>
  </section>

  <section class="bottom"></section>
</template>

<style scoped>
body {
  margin: 0;
  font-family: "Montserrat", sans-serif;
  width: 100%;
}

.page-header {
  display: block;
  width: 100%;
  margin: 0 auto;
  padding: 6rem 2rem;
  line-height: 1;
  background: linear-gradient(135deg, #881f48 0%, #611733 100%);
  color: white;
}

.page-header>* {
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
  grid-column: 3 / span 4;
}

.image-1 {
  grid-column: 1 / span 2;
}

.box-2 {
  grid-column: 2 / span 3;
}

.image-2 {
  grid-column: 6 / span 1;
}

.box-3 {
  grid-column: 3 / span 3;
}

.image-3 {
  grid-column: 1 / span 2;
}

.box-4 {
  grid-column: 1 / span 3;
}

.bottom {
  height: 50vh;
}
</style>

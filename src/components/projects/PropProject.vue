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
      Property management is often fragmented, relying on a patchwork of
      spreadsheets and isolated software. The goal with PropMG was to build a
      comprehensive, full-stack application that centralizes tracking for
      properties, tenants, leases, work orders, and accounting. We needed to
      create a unified ecosystem that streamlines operations for property
      managers and landlords, replacing chaos with an organized, data-driven
      dashboard.
    </p>

    <p>The core objectives were:</p>

    <ul>
      <li>Centralize property and tenant lifecycle management.</li>
      <li>Automate lease tracking, renewals, and expirations.</li>
      <li>Streamline maintenance requests and vendor coordination.</li>
      <li>
        Integrate a robust accounting system for granular financial oversight.
      </li>
    </ul>

    <p>
      The primary challenge was designing a system capable of handling complex
      relational data—like tenant screening info, lease histories, and
      portfolio-wide financial KPIs—while keeping the user interface clean and
      accessible for daily property management tasks.
    </p>

    <p>
      This required a highly scalable database schema, secure authentication
      workflows, and a highly modular frontend architecture that could grow with
      the application.
    </p>
    <!-- <img src="/propmg/logo.png" alt="PropMG Logo" class="header-bg-logo" /> -->
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
      <h2>PROPMG</h2>

      <div class="layout-container">
        <div class="box box-1">
          <h3>Architecting the System</h3>
          <p>
            To handle the rigorous demands of property management, the project
            required a reliable, scalable full-stack architecture. I utilized
            Vue 3 with the Composition API for a highly reactive frontend,
            paired with a Node.js and Express backend. To ensure data integrity
            and local development consistency, the database layer was
            containerized.
          </p>

          <p>The core technology stack:</p>

          <ul>
            <li>Vue 3, Vite, and Pinia for reactive state management.</li>
            <li>Node.js and Express.js configured with strict API routing.</li>
            <li>MySQL 8 database running seamlessly in Docker.</li>
            <li>Google OAuth 2.0, JWT, and bcryptjs for secure access.</li>
          </ul>

          <p>
            <strong>Key takeaway:</strong> A containerized, decoupled
            architecture provides the stable foundation needed to build secure,
            scalable business applications.
          </p>
        </div>

        <div class="image-1">
          <ImageStack />
        </div>

        <div class="box box-2">
          <h3>Property & Tenant Workflows</h3>
          <p>
            Managing the human element of real estate requires highly structured
            data. I built comprehensive modules to handle both the physical
            properties and the people living in them. This included everything
            from tracking move-in inventory to monitoring tenant preferences,
            credit scores, and prior eviction histories.
          </p>

          <ul>
            <li>
              Detailed property profiles with occupancy and inventory tracking.
            </li>
            <li>
              Deep tenant screening profiles including income and unique
              preferences.
            </li>
            <li>
              Lease lifecycle management from creation to renewal and move-out
              workflows.
            </li>
            <li>Automated tracking of upcoming lease expirations.</li>
          </ul>

          <br />
          <p>This structured approach ensures:</p>

          <ul>
            <li>Property managers never miss a lease renewal.</li>
            <li>Tenant histories and screening data are easily auditable.</li>
            <li>Occupancy gaps are minimized through proactive scheduling.</li>
          </ul>

          <p>
            By mapping these complex real-world relationships into a MySQL
            database, PropMG creates a seamless workflow for onboarding and
            managing tenants over years of occupancy.
          </p>
        </div>

        <!-- <img class="image-2" src="/propmg/tenants.png" /> -->

        <div class="box box-3">
          <h3>Operations & Accounting Engine</h3>
          <p>
            A property management system is only as good as its operational
            tools. I integrated a complete work order system allowing managers
            to submit, assign, and track maintenance requests through vendor
            pipelines. Parallel to this, I developed a robust accounting ledger
            to monitor financial health.
          </p>

          <ul>
            <li>
              Prioritized work order ticketing with in-depth status tracking.
            </li>
            <li>Vendor management and maintenance dispatch coordination.</li>
            <li>
              Granular accounting for rent payments, bills, and operational
              expenses.
            </li>
            <li>
              Automated financial statements with immediate CSV export
              capabilities.
            </li>
          </ul>

          <p>
            To make sense of this data, I built a dynamic KPI dashboard
            utilizing Chart.js. This provides a quick, portfolio-wide view of
            critical metrics: total rent collected, unpaid bills, overdue items,
            and completed work orders. It ensures managers always have their
            finger on the pulse of their business operations.
          </p>
        </div>

        <!-- <img class="image-3" src="/propmg/accounting.jpg" /> -->

        <div class="box box-4">
          <h3>Refactoring & UX Polish</h3>
          <p>
            As the platform grew to include complex views—such as a 1,600+ line
            ledger component—maintaining code quality became paramount. I
            designed and implemented a strict 6-phase refactoring strategy to
            extract reusable composables, modularize Pinia stores, and establish
            a cohesive design system.
          </p>

          <p>Recent architectural and UI improvements include:</p>
          <ul>
            <li>
              Implementation of clickable, filterable KPI stat cards on the
              dashboard.
            </li>
            <li>
              A smart pagination component deployed consistently across all data
              tables.
            </li>
            <li>
              Streamlined, quick-update workflows for modifying work order
              statuses.
            </li>
            <li>
              Extraction of shared UI components and integration of global CSS
              themes.
            </li>
          </ul>

          <p>
            This systematic refactoring not only reduced technical debt, but
            resulted in a snappy, highly responsive user interface that property
            managers can rely on without friction.
          </p>
        </div>

        <!-- <img class="image-4" src="/propmg/dashboard.jpg" /> -->

        <div class="box box-5">
          <h3>Engineering Impact</h3>
          <p>This project demonstrates core competencies in:</p>
          <ul>
            <li>
              Full-stack development from database schema to complete UI
              implementation.
            </li>
            <li>
              Complex relational database design using MySQL and Docker
              containerization.
            </li>
            <li>
              Advanced state management and component refactoring utilizing Vue
              3.
            </li>
            <li>
              Translating dense, real-world business logic into intuitive
              software tools.
            </li>
            <li>
              Integrating secure authentication and actionable data export
              pipelines.
            </li>
          </ul>
          <p>
            PropMG successfully transforms property management from a chaotic
            mix of documents into a centralized operational hub, built to scale
            alongside a growing real estate portfolio.
          </p>
          <a href="#" class="btn">Find out more</a>
        </div>
      </div>
    </div>
  </section>

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
  background: linear-gradient(135deg, #b32522 0%, #721816 100%);
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

@media (max-width: 1024px) {
  .container {
    padding: 0 2rem;
  }

  h2 {
    font-size: 48px;
    text-align: center;
  }

  .box {
    padding: 2.5rem;
  }

  /* Adjust Grid Spanning for medium screens */
  .box-1 {
    grid-column: 2 / span 5;
  }
  .box-2 {
    grid-column: 1 / span 4;
  }
  .box-3 {
    grid-column: 2 / span 5;
  }
  .box-4 {
    grid-column: 1 / span 4;
    margin-top: -100px; /* Reduce overlap */
  }

  /* Adjust image positions */
  .image-1 {
    margin-left: 20px;
    width: 250px;
  }
  .image-2 {
    margin-left: -400px;
    width: 250px;
  }
  .image-3 {
    margin-left: 0px;
    width: 250px;
  }

  .header-bg-logo {
    right: 2rem;
    height: 180px;
  }
}

/* Mobile Devices (Max Width: 768px) */
@media (max-width: 768px) {
  .page-header {
    padding: 4rem 1.5rem;
  }

  .header-bg-logo {
    display: none; /* Hide decorative logo on small screens to save space */
  }

  .container {
    padding: 0 1.5rem;
  }

  h2 {
    font-size: 36px;
    padding-top: 40px;
  }

  /* Collapse the grid to a single column stack */
  .layout-container {
    display: flex;
    flex-direction: column;
    gap: 3rem;
    padding-top: 4rem;
  }

  /* Reset all specialized grid and margin positioning */
  .box-1,
  .box-2,
  .box-3,
  .box-4,
  .box-5 {
    grid-column: auto;
    margin-top: 0 !important;
    width: 100%;
    padding: 2rem;
  }

  /* Reset image positioning to flow naturally between text blocks */
  .image-1,
  .image-2,
  .image-3 {
    margin: 0 auto !important;
    width: 80%;
    max-width: 300px;
    transform: scale(0.9) rotate(0deg) !important; /* Remove rotation for clean mobile look */
    display: flex;
    justify-content: center;
  }

  /* Ensure images fade in cleanly without the rotation skew on mobile */
  img.image-1.visible,
  img.image-2.visible,
  img.image-3.visible {
    transform: scale(1) rotate(0deg) !important;
  }

  /* Hide the SVG line on mobile as the staggered layout is gone */
  .line-svg {
    display: none;
  }

  /* Remove the minimum height requirement since the SVG is gone */
  #scroll-section {
    min-height: auto;
    padding-bottom: 4rem;
  }
}
</style>

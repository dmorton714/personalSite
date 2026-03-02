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
    <h1>Other Problems</h1>

    <p>
      While my primary projects focus on a deep-dive, my other work
      involves a wide array of <strong>supplementary technical skills</strong>.
      This section is designed to provide a high-level overview of the tools,
      methodologies, and experiments that round out my professional toolkit.
    </p>

    <p>Rather than a deep dive into a single project, these snapshots highlight:</p>
    <ul>
      <li>
        <strong>Rapid Prototyping:</strong> Moving from concept to functional
        MVP in tight windows.
      </li>
      <li>
        <strong>Secondary Stack Proficiency:</strong> Practical applications of
        supporting languages and frameworks.
      </li>
      <li>
        <strong>DevOps & Tooling:</strong> Automating the boring stuff to
        keep production moving.
      </li>
      <li>
        <strong>Technical Agility:</strong> The ability to pivot between
        frontend polish and backend optimization.
      </li>
    </ul>

    <p>
      <strong>The Big Picture:</strong> A modern developer isn't just a specialist;
      they are a problem solver who knows how to pick the right tool for the job.
    </p>
    <img src="/otherProjects/code.png" alt="Data Pipeline Diagram" class="header-bg-logo" />
  </header>

  <section id="scroll-section">
    <svg class="line-svg" preserveAspectRatio="xMidYMin slice" width="100%" fill="none" viewBox="-480 0 2300 2241">
      <path stroke="#3c0071" stroke-width="160" :stroke-dasharray="pathLength" :stroke-dashoffset="pathLength - pathLength * Math.min(scrollProgress * 1.4, 1)
        "
        d="M-841 100H584c124 0 225 101 225 225v0c0 124-101 225-225 225h-95a281 281 0 00-281 281v0c0 155 125 281 281 281h442c167 0 304 136 304 304v0c0 168-137 304-304 304H795a439 439 0 00-439 439v82"
        opacity=".45" />
    </svg>

    <div class="container">

      <div class="layout-container">
        <div class="box box-1">
          <h3>Database Migration</h3>
          <p>
            I transitioned a standalone data analysis workflow from a local
            environment to a containerized production pipeline. The goal was
            to move beyond temporary file storage by implementing a persistent,
            scalable <strong>MySQL</strong> backend.
          </p>

          <p>The pipeline architecture focuses on robustness and portability:</p>
          <ul>
            <li>
              <strong>Containerized Infrastructure:</strong> Leveraged
              <code>Docker</code> and <code>Docker Compose</code> to orchestrate
              the MySQL environment, ensuring parity between dev and production.
            </li>
            <li>
              <strong>Automated Schema Deployment:</strong> Built automated SQL
              initialization scripts to handle table creation and data modeling
              on container startup.
            </li>
            <li>
              <strong>Relational Mapping:</strong> Migrated flat-file logic into
              a relational structure, optimizing data types for faster querying
              and long-term storage.
            </li>
            <li>
              <strong>Persistent Volumes:</strong> Configured Docker volumes to
              maintain data integrity and persistence across container restarts
              and updates.
            </li>
          </ul>

          <br>
          <p>
            <strong>Key takeaway:</strong> By containerizing the database, I replaced
            manual data handling with a <strong>portable, reproducible infrastructure
              stack</strong> ready for cloud deployment.
          </p>
          <a href="https://github.com/dmorton714/db_migration" class="btn">Find out more</a>
        </div>

        <img class="image-1" src="/public/otherProjects/citydash.png" />

        <div class="box box-2">
          <h3>Learning Microservices</h3>
          <p>
            I engineered a high-performance data pipeline that decouples ingestion from
            visualization. By building a <strong>Go-based microservice</strong> to
            handle data retrieval, I ensured the system can efficiently pull and process
            large datasets before handing them off to the frontend.
          </p>

          <p>The architecture leverages a dual-stack approach:</p>
          <ul>
            <li>
              <strong>Go Ingestion Service:</strong> A dedicated microservice built
              to handle high-concurrency data fetching. It manages the complexity of
              connecting to external sources and normalizing raw data into a structured format.
            </li>
            <li>
              <strong>Concurrent Processing:</strong> Utilized Go's performance to
              minimize bottlenecks during the "pull" phase, ensuring the data is ready
              and validated before the dashboard ever loads.
            </li>
            <li>
              <strong>Streamlit Integration:</strong> Built a reactive Python dashboard
              that consumes the processed data, providing an interactive interface for
              real-time analysis and filtering.
            </li>
            <li>
              <strong>Modular Decoupling:</strong> By separating the ingestion engine (Go)
              from the UI (Python), I created a system where either component can be
              scaled or updated without breaking the entire pipeline.
            </li>
          </ul>

          <br>
          <p>
            <strong>Key takeaway:</strong> This project demonstrates a
            <strong>production-mindset architecture</strong>, using Go for its
            computational efficiency and Python for its rapid visualization capabilities.
          </p>
          <a href="https://github.com/dmorton714/ForeclosureDashboard-/tree/main" class="btn">Find out more</a>
        </div>

        <img class="image-2" src="/public/otherProjects/foreclosure.png" />

        <div class="box box-3">
          <h3>Pandas PR</h3>
          <p>
              This project is a custom utility package designed to convert pandas 
              DataFrames and Series into markdown-formatted tables. It provides 
              a lightweight alternative to pandas' built-in methods without the 
              need to install external dependencies like <code>tabulate</code>.
            </p>
            <p>Building this utility demonstrated critical Python engineering concepts:</p>
            <ul>
              <li>
                <strong>Object Extension:</strong> Extending native Pandas objects by 
                attaching custom methods directly to the DataFrame and Series classes.
              </li>
              <li>
                <strong>Dependency Minimization:</strong> Writing raw Python logic to handle 
                string formatting and table generation without relying on bloated external libraries.
              </li>
              <li>
                <strong>Flexible Signatures:</strong> Implementing dynamic arguments allowing 
                users to filter specific columns or rename headers on the fly.
              </li>
              <li>
                <strong>Module Packaging:</strong> Structuring the code so it can be 
                cleanly imported and utilized in both scripts and Jupyter Notebooks.
              </li>
            </ul>
            <p>
              <strong>Key takeaway:</strong> Building custom tooling teaches you how to 
              interact with the internals of popular libraries like Pandas, reducing overhead 
              and improving the developer experience.
            </p>
          <a href="https://github.com/dmorton714/markDown" class="btn">Find out more</a>
        </div>

        <img class="image-3" src="/public/otherProjects/markdown.png" />

        <!-- Add more projects here -->

        <!-- <div class="box box-4">
          <h3>Engineering Impact</h3>
          <p>
            This project represents the transition from academic data science to
            <strong>Production Engineering</strong>. What began as a manual
            reporting hurdle was transformed into a modular, lightweight data
            pipeline designed for scalability and maintainability.
          </p>
          <p>This project demonstrates:</p>
          <ul>
            <li>
              <strong>Automation in environments:</strong> Architecting reliable
              data retrieval workflows.
            </li>
            <li>
              <strong>Practical data engineering and normalization:</strong>
              Transforming raw, inconsistent data into high-fidelity, structured
              models.
            </li>
            <li>
              <strong>Analytical modeling using structured data:</strong>
              Implementing logic that derives high-value business metrics from
              raw inputs.
            </li>
            <li>
              <strong>Clear separation between data pipeline and presentation layer:</strong>
              Moving logic out of fragile notebooks and into a professional,
              modular Python architecture.
            </li>
            <li>
              <strong>Building internal tooling to improve operational visibility:</strong>
              Creating systems that provide stakeholders with immediate, automated insights.
            </li>
          </ul>
          <p>
            It began as a automation and replication problem. It became a lightweight data
            pipeline with a decision-support interface.
          </p>
          <p>
            <strong>Key takeaway:</strong> By focusing on modularity and the <code>main.py</code>
            orchestrator, I built a system that is version-control ready and capable of deployment
            in a cloud environment.
          </p>
          <a href="https://github.com/dmorton714/pokemon_analysis_project" class="btn">Find out more</a>
        </div> -->
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
  position: relative;
  display: block;
  width: 100%;
  margin: 0 auto;
  padding: 6rem 2rem;
  line-height: 1;
  background: linear-gradient(135deg, #006803 0%, #005203 100%);
  color: white;
}

.header-bg-logo {
  position: absolute;
  bottom: 1rem;
  right: 2rem;
  height: 550px;
  width: auto;
  opacity: 0.25 !important;
  pointer-events: none;
  z-index: 1;
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
  color: #3c0071;
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
  position: relative;
  z-index: 2;
}

.image-1 {
  grid-column: 1 / span 2;
  width: 600px;
  margin-left: -20px;
  margin-top: -320px;
  z-index: 1;
  transform: scale(0.8) rotate(-20deg);
}

img.image-1.visible {
  opacity: 1;
  transform: scale(1.1) rotate(-20deg);
}

.box-2 {
  grid-column: 2 / span 3;
  z-index: 2;
}

.image-2 {
  grid-column: 5 / span 3;
  width: 400px;
  margin-left: -20px;
  margin-top: 60px;
  z-index: 1;
  transform: scale(0.8) rotate(12deg);
}

img.image-2.visible {
  opacity: 1;
  transform: scale(1.1) rotate(12deg);
}

.box-3 {
  grid-column: 3 / span 4;
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
  grid-column: 1 / span 4;
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
  .box-1 { grid-column: 2 / span 5; }
  .box-2 { grid-column: 1 / span 4; }
  .box-3 { grid-column: 2 / span 5; }
  .box-4 { 
    grid-column: 1 / span 4; 
    margin-top: -100px; /* Reduce overlap */
  }

  /* Adjust image positions */
  .image-1 { margin-left: 20px; width: 250px; }
  .image-2 { margin-left: -400px; width: 250px; }
  .image-3 { margin-left: 0px; width: 250px; }
  
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
  .box-1, .box-2, .box-3, .box-4, .box-5 {
    grid-column: auto;
    margin-top: 0 !important;
    width: 100%;
    padding: 2rem;
  }

  /* Reset image positioning to flow naturally between text blocks */
  .image-1, .image-2, .image-3 {
    margin: 0 auto !important;
    width: 80%;
    max-width: 300px;
    transform: scale(0.9) rotate(0deg) !important; /* Remove rotation for clean mobile look */
    display: flex;
    justify-content: center;
  }
  
  /* Ensure images fade in cleanly without the rotation skew on mobile */
  img.image-1.visible, img.image-2.visible, img.image-3.visible {
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

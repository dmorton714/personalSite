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
      Many Data Science students graduate from bootcamps with high proficiency
      in <strong>Jupyter Notebooks</strong>, but little exposure to
      <strong>Production Python</strong>. While notebooks are excellent for
      experimentation, they often lead to "spaghetti code" that is difficult to
      automate, version control, or deploy in a professional environment. With
      this, I worked with data that all my coworkers understood.
    </p>

    <p>The core challenges addressed in this project were:</p>
    <ul>
      <li>Lack of experience with modular <code>.py</code> file structures</li>
      <li>
        Difficulty understanding how to pass data between separate scripts
      </li>
      <li>
        Uncertainty regarding the role of a <code>main.py</code> entry point
      </li>
      <li>
        Transitioning from a "Run All" manual workflow to an automated pipeline
      </li>
    </ul>

    <p>
      <strong>Key takeaway:</strong> To work in a modern tech stack, a developer
      must move beyond the notebook and understand how to build a modular,
      scalable codebase.
    </p>
    <img src="/pokeProject/pokef.png" alt="Data Pipeline Diagram" class="header-bg-logo" />
  </header>

  <section id="scroll-section">
    <svg class="line-svg" preserveAspectRatio="xMidYMin slice" width="100%" fill="none" viewBox="-480 0 2300 2241">
      <path stroke="#ffcb05" stroke-width="160" :stroke-dasharray="pathLength" :stroke-dashoffset="pathLength - pathLength * Math.min(scrollProgress * 1.4, 1)
        "
        d="M-841 100H584c124 0 225 101 225 225v0c0 124-101 225-225 225h-95a281 281 0 00-281 281v0c0 155 125 281 281 281h442c167 0 304 136 304 304v0c0 168-137 304-304 304H795a439 439 0 00-439 439v82"
        opacity=".45" />
    </svg>

    <div class="container">
      <h2>Notebook to Production ETL Pipeline</h2>

      <div class="layout-container">
        <div class="box box-1">
          <h3>Phase 1: Prototyping & Pipeline Logic</h3>
          <p>
            The project began within a Jupyter Notebook to establish the core
            logic. This allowed students to see the immediate output of the API
            calls and the transformation of raw data into insights.
          </p>
          <p>The logic followed a standard production sequence:</p>
          <ul>
            <li>
              <strong>Data Ingestion:</strong> Authenticating and fetching live
              data from a REST API.
            </li>
            <li>
              <strong>Data Cleaning:</strong> Handling missing values and
              standardizing formats.
            </li>
            <li>
              <strong>Feature Engineering:</strong> Using existing data to
              calculate new, high-value metrics.
            </li>
            <li>
              <strong>Visualization:</strong> Generating a standard set of plots
              for stakeholder review.
            </li>
          </ul>
          <p>
            <strong>Key takeaway:</strong> The notebook serves as the "drafting
            board" where the logic is proven before it is hardened into scripts.
          </p>
        </div>

        <img class="image-1" src="https://assets.codepen.io/732/matthew-deltoro-LdFvvpjnB2A-unsplash-800.jpg" />

        <div class="box box-2">
          <h3>Phase 2: Modular Architecture</h3>
          <p>
            Once the logic was validated, we broke the notebook into a
            professional directory structure. This taught students how to
            organize a project so that different sections of code can be run or
            updated independently.
          </p>
          <p>The project was refactored into specialized modules:</p>
          <ul>
            <li>
              <code>get_data.py</code>: Isolated the API logic to keep the
              project clean. Utilized functions to fetch and return raw data in
              a standardized format. Added error handling and logging for robust
              data retrieval.
            </li>
            <li>
              <code>clean_data.py</code>: Housed the cleaning and feature
              engineering logic. Functions were designed to be reusable and
              parameterized, allowing for flexible data processing if the
              project evolved.
            </li>
            <li>
              <code>feature_engineering.py</code>: Here we created functions to
              compute new metrics from the raw data, such as BMI data for each
              Pokemon. This separation allowed for easy updates to the feature
              logic without affecting data retrieval or visualization.
            </li>
            <li>
              <code>create_plots.py</code>: Contained reusable functions for
              plotting and saving charts. This modularity meant that if we
              wanted to change the visualization style or add new plots, we
              could do so without touching the data processing code.
            </li>
          </ul>
          <p>
            <strong>Key takeaway:</strong> Modular code is predictable and
            allows multiple developers to work on different parts of the project
            simultaneously without conflict.
          </p>
        </div>

        <img class="image-2" src="https://assets.codepen.io/732/viviana-rishe-6fNZ7QtXiCs-unsplash-800.jpg" />

        <div class="box box-3">
          <h3>Phase 3: The main.py Orchestrator</h3>
          <p>
            The final piece of the puzzle was the implementation of a
            <code>main.py</code> file. This script acts as the Conductor,
            importing the functions from the modules created in Phase 2 and
            executing them in the correct order.
          </p>
          <p>This phase demonstrated critical production concepts:</p>
          <ul>
            <li>
              The <code>if name == "main":</code> boilerplate for script
              execution
            </li>
            <li>Efficiently passing DataFrames as objects between functions</li>
            <li>
              Using a single terminal command to run an entire end-to-end
              workflow
            </li>
            <li>Implementing basic logging to track the pipeline's progress</li>
          </ul>
          <p>
            <strong>Key takeaway:</strong> A well-structured
            <code>main.py</code> makes the project portable and ready for
            deployment in a cloud environment or a scheduled task.
          </p>
        </div>

        <img class="image-3" src="https://assets.codepen.io/732/colton-sturgeon-FiCPutl_aog-unsplash-800.jpg" />

        <div class="box box-4">
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
  position: relative;
  display: block;
  width: 100%;
  margin: 0 auto;
  padding: 6rem 2rem;
  line-height: 1;
  background: linear-gradient(135deg, #2a75bb 0%, #3c5aa6 100%);
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
  color: #ffcb05;
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
  grid-column: 3 / span 3;
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
  grid-column: 1 / span 4;
}

.bottom {
  height: 50vh;
}
</style>

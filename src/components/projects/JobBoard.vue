<script setup>
import { ref, onMounted, onUnmounted } from "vue";
import ImageStackJob from "./ImageStackJob.vue";
import ImageStackDone from "./ImageStackDone.vue";

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
      The non-profit organization <strong>Code:You</strong> faced a major hurdle
      in student placement: job opportunities were scattered across multiple
      Slack channels, leading to "link rot" and invisible data. Fresh bootcamp
      graduates struggled to find relevant roles, and the staff had no way to
      track which skills were actually in demand.
    </p>

    <p>The core challenges addressed in this project were:</p>
    <ul>
      <li>
        <strong>Lack of Centralization:</strong> Important job leads were lost
        in fast-moving chat histories.
      </li>
      <li>
        <strong>Data Expiration:</strong> No system existed to prune dead links,
        leading to a poor user experience for job seekers
      </li>
      <li>
        <strong>Visibility Gaps:</strong> Leadership had no metrics on salary
        trends, regional demand, or required tech stacks
      </li>
      <li>
        <strong>Junior Skill Gaps:</strong> Coordinating 9 junior developers
        required a technical roadmap that balanced learning with
        production-grade delivery
      </li>
    </ul>
    <p>
      <strong>Key takeaway:</strong> We didn't just build a website; we built a
      <strong>labor market intelligence tool</strong> that allowed students to
      identify and fill their own skill gaps based on real-time data
    </p>
    <img src="/public/jobboard/cy-logo-stacked-black@2x.png" alt="CodeYou Logo" class="header-bg-logo" />
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
            As Project Manager and Technical Advisor, I led the team through a
            five-stage deployment to move from manual messaging to an automated,
            data-driven platform.
          </p>
          <ul>
            <li>
              <strong>1. Internal Ingestion & Validation:</strong> We developed
              a standardized staff input form to replace unstructured Slack
              posts. This ensured every job entry contained critical metadata
              like salary, region, and required languages.
            </li>
            <li>
              <strong>2. Redundant Data Architecture:</strong> We designed a
              hybrid storage solution using <strong>MongoDB</strong> for
              high-performance querying, with a
              <strong>Google Sheets failover</strong>. This provided the
              non-profit staff with a familiar interface for manual audits while
              maintaining a professional database backend.
            </li>
            <li>
              <strong>3. Automated Lifecycle Management:</strong> To solve the
              "dead link" problem, we implemented a 30-day expiration logic.
              Posts were automatically flagged or archived after 30 days,
              ensuring students only spent time on active opportunities.
            </li>
            <li>
              <strong>4. Analytical Dashboarding:</strong> We built a
              decision-support interface that aggregated job data. This allowed
              students to visualize demand by region (State vs. Remote) and
              identify the most requested languages/skills in the current
              market.
            </li>
            <li>
              <strong>5. Technical Mentorship & Code Review:</strong> Beyond the
              architecture, I managed the 9-developer sprint cycle, stepping in
              to resolve blockers in database schema design and UI/UX
              consistency to ensure the final product was production-ready.
            </li>
          </ul>
          <a href="#" class="btn">Find out more</a>
        </div>

        <img class="image-1" src="/public/jobboard/slack.png" />

        <div class="box box-2">
          <h3>Breaking the Project Into Executable Parts</h3>
          <p>
            When the project started, the scope was vague. “We need a job board” meant different
            things to different people. With nine junior developers, that ambiguity would have
            turned into chaos quickly.
          </p>

          <p>
            So the first thing I did was break the system into clear parts:
          </p>
          <p>
          <ul>
            <li>How jobs enter the system</li>
            <li>How they’re stored</li>
            <li>How they expire</li>
            <li>How they’re queried</li>
            <li>How they’re displayed</li>
          </ul>
          </p>
          <br>
          <p>
            Each part became its own set of tickets. Instead of assigning big features, I assigned small,
            concrete tasks like building validation rules, defining schema fields, or implementing expiration
            logic. That made it easier for newer developers to contribute without stepping on each other.
          </p>

          <p>
            The work moved forward because everyone knew exactly what they were building and why it mattered to the
            larger system.
          </p>
        </div>

        <div class="image-2">
          <ImageStackJob />
        </div>

        <div class="box box-3">
          <h3>Managing the Codebase Day to Day</h3>
          <p>
            Once development began, my role shifted into coordination and correction.
          </p>

          <p>
            We ran lightweight sprints and used pull requests for everything. Every PR came
            through me. Different developers had different naming styles, different approaches 
            to state management, and different assumptions about validation. Without review, the
            codebase would have fragmented.
          </p>

          <p>
            A lot of my time was spent:
          </p>

          <p>
          <ul>
            <li>Refactoring duplicate logic</li>
            <li>Aligning database queries with the schema</li>
            <li>Fixing edge cases in expiration rules</li>
            <li>Standardizing structure on the frontend</li>
          </ul>
          </p>

          <br>

          <p>
            When someone got stuck on a MongoDB query or middleware validation, I paired
            with them and worked through it. The goal wasn’t just to fix the issue, but to
            make sure they understood the pattern we were establishing.
          </p>

          <p>
            By the midpoint of the project, the code felt unified instead of stitched together.
          </p>
        </div>

        <div class="image-3">
          <ImageStackDone />
        </div>

        <div class="box box-4">
          <h3>Keeping the System Stable</h3>
          <p>
            As features accumulated, stability became the priority.
          </p>

          <p>
            We introduced expiration logic, failover storage with Google Sheets, and stricter
            input validation. Those decisions came from watching how real users interacted
            with the system and noticing where it could break.
          </p>

          <p>
            Some of the work wasn’t visible in the UI at all.
          </p>

          <p>
          <ul>
            <li>Tightening schema rules</li>
            <li>Cleaning up inconsistent records</li>
            <li>Preventing invalid submissions from reaching the database</li>
            <li>Revisiting edge cases discovered during testing</li>
          </ul>
          </p>
        </div>

        <div class="box box-3">
          <h3>Engineering Impact</h3>

          <p>This project demonstrates:</p>
          <ul>
            <li>
              <strong>Strategic Project Management:</strong> Leading a large
              team of junior developers through a complex SDLC.
            </li>
            <li>
              <strong>Fault-Tolerant System Design:</strong> Implementing
              database failovers to ensure 100% uptime for non-profit
              operations.
            </li>
            <li>
              <strong>Automation in environments without APIs:</strong> Bridging
              the gap between manual staff input and automated public displays.
            </li>
            <li>
              <strong>Decision-Support Engineering:</strong> Turning raw job
              posts into actionable insights for student career pivots.
            </li>
            <li>
              <strong>Building internal tooling to improve operational
                visibility:</strong>
              Providing leadership with the first-ever clear view of their
              graduates' hiring landscape.
            </li>
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

.header-bg-logo {
  position: absolute;
  bottom: .2rem;
  right: 10rem;
  height: 250px;
  width: auto;
  opacity: 0.15 !important;
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
  position: relative;
  z-index: 2;
}

.image-1 {
  grid-column: 1 / span 2;
  width: 350px;
  margin-left: 90px;
  margin-top: -180px; 
  z-index: 1; 
  transform: scale(0.8) rotate(-22deg); 
}

img.image-1.visible {
  opacity: 1;
  transform: scale(1.1) rotate(-22deg);
}

.box-2 {
  grid-column: 1 / span 3;
  position: relative;
  z-index: 2;
}

.image-2 {
  grid-column: 6 / span 1;
  width: 350px;
  margin-left: -590px;
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
  grid-column: 1 / span 2;
  width: 350px;
  margin-left: -150px;
  margin-top: -360px; 
  z-index: 1; 
  transform: scale(0.8) rotate(-12deg); 
}

img.image-3.visible {
  opacity: 1;
  transform: scale(1.1) rotate(-12deg);
}

.box-4 {
  grid-column: 1 / span 3;
  margin-top: -250px;
  position: relative;
  z-index: 5;
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

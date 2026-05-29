<script setup>
import { ref, onMounted, onUnmounted } from "vue";
import ImageStack from "./ImageStackStaaty.vue";
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
      The goal was to build a sports platform unlike anything else on the
      market—a comprehensive, data-driven hub that offers deep insights while
      keeping fans highly engaged. To achieve this, we needed to engineer a
      robust reporting system to deliver clean, structured data, paired
      seamlessly with interactive social features. The app goes far beyond a
      standard stats dashboard; it is an immersive experience designed to bring
      fans closer to the game.
    </p>

    <p>The core objectives were:</p>

    <ul>
      <li>
        Architect a scalable framework for handling high-volume sports data.
      </li>
      <li>Design highly responsive, interactive tools for user engagement.</li>
      <li>
        Curate and maintain a comprehensive database of sports statistics.
      </li>
      <li>Integrate compelling social and community features.</li>
    </ul>

    <p>
      Our primary challenge was balancing power with accessibility. We needed to
      translate complex data into digestible insights without overwhelming the
      user. This required thoughtful UI/UX design and a strategic approach to
      presenting data in a way that is both visually engaging and intuitive.
    </p>

    <img
      src="/staaty/staaty_logo_withtype.png"
      alt="Staaty Logo"
      class="header-bg-logo"
    />
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
      <h2>STAATY</h2>

      <div class="layout-container">
        <div class="box box-1">
          <h3>Creating the Platform</h3>
          <p>
            The project began with a deep competitive analysis of the market. I
            identified a clear gap: existing platforms either offered deep data
            with poor usability, or great UX with shallow data. Drawing
            inspiration from financial data terminals, we set out to build a
            platform that merged comprehensive analytics with an exceptional
            user experience.
          </p>

          <p>Our prototyping process:</p>

          <ul>
            <li>
              Conducted comprehensive market research to identify user pain
              points.
            </li>
            <li>Developed low-fidelity mockups to test layouts.</li>
            <li>Built functional mini-dashboards to validate our concepts.</li>
            <li>Transitioned into full platform development.</li>
          </ul>

          <p>
            <strong>Key takeaway:</strong> Iterate quickly, gather feedback
            early, and always focus on delivering tangible value to the users.
          </p>
        </div>

        <div class="image-1">
          <ImageStack />
        </div>

        <div class="box box-2">
          <h3>Data Creation & Normalization</h3>
          <p>
            We initially targeted emerging sports leagues that boasted
            passionate fan bases but lacked centralized data platforms. Sourcing
            this data required a multi-pronged approach: capturing data from
            official league websites, utilizing third-party aggregators, and
            implementing an AI-driven engine to normalize everything into a
            consistent format.
          </p>

          <ul>
            <li>Identified and integrated reliable third-party data APIs.</li>
            <li>
              Engineered custom scraping scripts for fragmented online data.
            </li>
            <li>
              Deployed an AI platform for intelligent data capture and
              normalization.
            </li>
            <li>Filled historical gaps through manual data entry.</li>
          </ul>

          <br />
          <p>Using Python, we built a highly robust data capture pipeline:</p>

          <ul>
            <li>Developed automated scripts to run scheduled data pulls.</li>
            <li>
              Designed strict normalization workflows to ensure data integrity.
            </li>
            <li>
              Built a scalable pipeline capable of handling future league
              expansions.
            </li>
          </ul>

          <p>
            This architecture yielded a clean, structured dataset, forming the
            reliable foundation needed for advanced analytics and feature
            development.
          </p>
        </div>

        <img class="image-2" src="/staaty/data.png" />

        <div class="box box-3">
          <h3>Analytical Layer & Reusable Structures</h3>
          <p>
            With a structured database in place, the next step was building the
            analytical engine. To support a wide variety of sports and data
            types, I engineered a highly flexible system based on reusable
            functions and modular UI components.
          </p>

          <ul>
            <li>
              Developed reusable analytical functions for rapid data processing.
            </li>
            <li>
              Established unified data access patterns across the platform.
            </li>
            <li>
              Created standardized, modular data visualization components.
            </li>
            <li>
              Implemented a cohesive design system to ensure UI consistency.
            </li>
          </ul>

          <p>
            Because the application supports a diverse range of datasets, it was
            crucial to have a flexible analytical layer that could adapt on the
            fly. Meanwhile, the reusable components and strict design system
            ensured we could maintain a seamless user experience even as we
            rapidly deployed new features.
          </p>

          <p>
            <strong>The result:</strong> Scalable data processing paired with a
            cohesive user interface that keeps fans engaged.
          </p>
        </div>

        <img class="image-3" src="/staaty/staaty.png" />

        <div class="box box-4">
          <h3>Interactive Dashboard & Visualization</h3>
          <p>
            The final hurdle was presentation: how do we make complex data fun
            and accessible? We transitioned from static reporting to an
            exploratory model, building a dynamic dashboard that empowers users
            to manipulate the data through intuitive filters, sorting, and rich
            visual storytelling.
          </p>

          <p>The dashboard enabled the following capabilities:</p>
          <ul>
            <li>
              Customized data exploration through advanced filtering and
              sorting.
            </li>
            <li>
              Interactive visualizations that simplify dense, complex
              statistics.
            </li>
            <li>
              Real-time dynamic updates reflecting the latest game insights.
            </li>
            <li>
              Integrated social features allowing fans to chat and watch
              historical events simultaneously.
            </li>
          </ul>

          <p>
            By empowering users to interact with the data directly, the platform
            successfully positioned itself as the ultimate "second screen" for
            sports fans.
          </p>
        </div>

        <img class="image-4" src="/staaty/ufc.png" />

        <div class="box box-5">
          <h3>Engineering Impact</h3>
          <p>This project demonstrates core competencies in:</p>
          <ul>
            <li>
              Architecting a comprehensive, full-stack data platform from
              scratch.
            </li>
            <li>
              Managing complex data capture, normalization, and pipeline
              scaling.
            </li>
            <li>
              Designing intuitive, interactive dashboards and data
              visualizations.
            </li>
            <li>
              Establishing reusable components to future-proof the application.
            </li>
            <li>Delivering a cohesive, highly engaging user experience.</li>
          </ul>
          <p>
            What began as a reporting challenge evolved into a fully realized
            platform that brings fans closer to the game—ready to set a new
            standard for engagement in the sports industry.
          </p>
          <a href="https://staaty.com" target="_blank" class="btn">Find out more</a>
        </div>

        <a href="https://staaty.com" target="_blank" class="image-5">
          <img src="/staaty/staaty_logo_withtype.png" alt="Staaty Logo" />
        </a>
      </div>
    </div>
  </section>

  <!-- <section class="bottom"></section> -->
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
  background: linear-gradient(135deg, #4e4e4e 0%, #8e8e8e 100%);
  color: white;
}

.header-bg-logo {
  position: absolute;
  bottom: 1rem;
  right: 1rem;
  height: 400px;
  width: auto;
  opacity: 100 !important;
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
  color: rgb(255, 255, 255);
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
  padding-bottom: 2rem;
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

.box-5 {
  grid-column: 4 / span 3;
  z-index: 2;
}

.image-5 {
  grid-column: 1 / span 2;
  width: 500px;
  margin-left: 180px;
  margin-top: -380px;
  z-index: 1;
  transform: scale(0.8) rotate(-15deg);
  display: flex;
  align-items: center;
  justify-content: center;
  filter: drop-shadow(2px 2px 0px white) 
          drop-shadow(-2px -2px 0px white) 
          drop-shadow(2px -2px 0px white) 
          drop-shadow(-2px 2px 0px white)
          drop-shadow(0 20px 40px rgba(0, 0, 0, 0.3));
}

.image-5 img {
  width: 100%;
  height: auto;
}

.image-5.visible {
  opacity: 1;
  transform: scale(1.1) rotate(-15deg);
}

.dashboard-preview-wrapper {
  position: relative;
  width: 100%;
  height: auto;
  margin: 4rem auto;
  overflow: hidden;
  box-shadow: 0 20px 50px rgba(0, 0, 0, 0.3);
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

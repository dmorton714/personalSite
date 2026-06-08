<script setup>
import { ref, computed } from 'vue'
import DmLogo from './DmLogo.vue' // Adjust the path if necessary

//  FILTER STATE 
const categories = ['All', 'Software Developer', 'Data Analytics', 'Project Management', 'Consulting']
const selectedCategory = ref('All')

const matchesFilter = (tags) => {
  if (selectedCategory.value === 'All') return true
  return tags.includes(selectedCategory.value)
}

//  EXPORT FUNCTION 
const exportToPDF = () => {
  window.print() // The @media print CSS handles the formatting
}

//  RESUME DATA
const contactInfo = {
  location: 'Louisville, KY',
  phone: '502.262.2642',
  email: 'Danny.Morton714@gmail.com'
}

const education = [
  {
    school: 'Western Kentucky University',
    location: 'Bowling Green, KY',
    degree: 'Bachelor of Science, Political Science',
    year: '2010'
  },
  {
    school: 'Jefferson Community And Technical College',
    location: 'Louisville, KY',
    degree: 'Associates of Applied Science — Graphic Design & Web Development',
    year: '2013'
  }
]

const jobs = [
  {
    company: 'Napster',
    location: 'Remote',
    title: 'QA Automation Engineer / Software Engineer',
    dates: '2026 – Current',
    bullets: [
      { text: 'Architected and developed automated testing scripts using Python and Selenium to streamline regression testing and validate core website functionality for a learning development platform.', tags: ['Software Developer', 'Data Analytics'] },
      { text: 'Configured GitHub Actions to automatically trigger Selenium test suites, establishing a hands-off continuous testing pipeline that routes formatted failure tickets directly into the development team\'s workflow.', tags: ['Software Developer', 'Project Management'] },
      { text: 'Engineered a lightweight QA reporting dashboard by piping automated test results directly into Google Sheets via API, providing accessible real-time metrics to cross-functional teams.', tags: ['Data Analytics', 'Consulting'] },
      { text: 'Provided actionable UX and WCAG accessibility recommendations, bridging the gap between QA findings and strategic product improvements.', tags: ['Consulting', 'Software Developer'] },
      { text: 'Designed a low-overhead incident logging system prioritizing rapid deployment and cross-functional accessibility over complex architecture.', tags: ['Software Developer', 'Project Management'] }
    ]
  },
  {
    company: 'Staaty',
    location: 'Remote',
    title: 'Chief Technology Officer / Lead Full Stack Engineer',
    dates: '2024 – Current',
    bullets: [
      { text: 'Accelerated time-to-market by strategically selecting lightweight, high-speed technologies (DuckDB, Node.js) to deliver the initial platform MVP within 90 days; successfully demoed to major professional sports organizations.', tags: ['Software Developer', 'Project Management'] },
      { text: 'Architected and co-executed a backend infrastructure migration from a Node/DuckDB stack to a highly scalable FastAPI and PostgreSQL architecture, onboarding a secondary engineer mid-cycle to execute the transition.', tags: ['Software Developer', 'Data Analytics', 'Project Management'] },
      { text: 'Engineered AI-driven content pipelines using Python and LLM APIs to autonomously generate dynamic player bios and statistical performance breakdowns from raw data, increasing average session duration by 15%.', tags: ['Data Analytics', 'Software Developer'] },
      { text: 'Engineered custom data visualization packages integrating ChartJS within a Vue frontend to translate complex sports statistics into digestible tables and plots.', tags: ['Software Developer', 'Data Analytics'] },
      { text: 'Integrated live game streaming and real-time community chat via WebSockets, driving concurrent user engagement during sporting events.', tags: ['Software Developer'] },
      { text: 'Led high-stakes product demonstrations for major professional sports organizations, translating complex technical architecture into clear, business-driven value propositions.', tags: ['Consulting', 'Project Management'] },
      { text: 'Engineered crawlable site architecture and implemented JSON-LD structured data, scaling organic traffic 300% (50 to 200+ daily sessions) in 8 weeks.', tags: ['Software Developer', 'Data Analytics'] }
    ]
  },
  {
    company: 'Code:You (Nonprofit coding bootcamp)',
    location: 'Louisville, KY',
    title: 'Technical Project Lead / Program Manager',
    dates: '2023 – Current',
    bullets: [
      { text: 'Directed portfolio-level strategy for 20 concurrent nonprofit web application projects using Monday.com and Kanban boards, managing complete SDLC from database schema design to cloud deployment.', tags: ['Project Management'] },
      { text: 'Conducted deep-dive discovery sessions with nonprofit stakeholders to identify operational bottlenecks and architect tailored MVP solutions, leading iterative presentations to lock down project scope prior to development.', tags: ['Consulting', 'Project Management'] },
      { text: 'Spearheaded curriculum development for C#, JavaScript, AI, AWS, and Python; leveraged data-driven strategies to improve student retention and course completion by ~10%.', tags: ['Data Analytics', 'Project Management', 'Software Developer'] },
      { text: 'Engineered custom automation workflows via Python and Zapier integrating third-party APIs, reducing manual data entry workloads by 10+ hours per week.', tags: ['Data Analytics', 'Software Developer'] },
      { text: 'Developed data pipelines and interactive dashboards using Python, Pandas, Tableau, and Streamlit to translate raw program data into actionable insights for leadership.', tags: ['Data Analytics'] },
      { text: 'Architected technical SEO migrations for legacy nonprofit sites, achieving a 30% average increase in indexable pages and organic visibility.', tags: ['Software Developer', 'Consulting'] },
      { text: 'Managed and mentored cohorts of up to 54 mentors and 600+ students; hosted office hours and live demos covering JavaScript, Python, C#, and Docker.', tags: ['Consulting', 'Project Management'] }
    ]
  },
  {
    company: 'Best One Tires',
    location: 'Louisville, KY',
    title: 'IT Director / Manager & Web Systems Developer',
    dates: '2021 – Current',
    bullets: [
      { text: 'Renegotiated enterprise credit card processing, ISP fiber contracts, and telecom agreements, securing a custom fee model that drove over $200K in total annual cost savings.', tags: ['Consulting', 'Project Management'] },
      { text: 'Designed and deployed real-time BI dashboards using Python and SQL to monitor inventory and sales, averting supply chain bottlenecks and contributing to 15%+ business growth.', tags: ['Data Analytics'] },
      { text: 'Directed end-to-end cloud migration of legacy on-premise SQL servers and a self-hosted SaaS platform (Maddenco), eliminating hardware overhead and end-of-life systems; reduced annual costs by $20K.', tags: ['Project Management', 'Consulting'] },
      { text: 'Reengineered site architecture and deployed geo-specific landing pages with schema markup, scaling daily organic traffic from 20 to 250+ users.', tags: ['Software Developer', 'Data Analytics'] },
      { text: 'Hardened web security by migrating infrastructure to AWS/Azure and configuring Cloudflare WAF, successfully mitigating data scraping and brute-force attacks.', tags: ['Project Management', 'Consulting'] },
      { text: 'Orchestrated cellular migration of 200+ field devices via Apple DEP and transitioned to hosted VoIP, cutting telecom costs by $24K/year and enhancing sales productivity.', tags: ['Project Management'] },
      { text: 'Architected automated multi-location data syncing pipelines bridging a legacy POS system with modern web reporting tools, saving employees 2–3 hours of manual entry daily.', tags: ['Data Analytics', 'Software Developer'] },
      { text: 'Standardized core IT procedures through rigorous documentation and automated routine deployment workflows via RMM scripting, saving 20+ manual labor hours per month.', tags: ['Project Management', 'Consulting'] }
    ]
  },
  {
    company: 'ADI (Resideo / Honeywell)',
    location: 'Louisville, KY',
    title: 'Systems Developer / Technical Hardware Support Specialist',
    dates: '2019 – 2021',
    bullets: [
      { text: 'Automated operational tasks using SQL and custom scripting, reducing a 40-hour per-order manual process to a 1-hour automated workflow and doubling departmental client onboarding capacity.', tags: ['Data Analytics', 'Software Developer', 'Project Management'] },
      { text: 'Developed internal diagnostic tools for support teams, improving resolution speed for complex client deployments by 25%.', tags: ['Software Developer', 'Consulting'] },
      { text: 'Programmed over 1,700 IP cameras, NVRs, and SQL-based systems for plug-and-play deployment, improving customer experience and reducing post-sale support needs.', tags: ['Project Management'] },
      { text: 'Contributed to Salesforce and internal software optimization, enabling cross-departmental BI reporting and real-time operational transparency across sales teams.', tags: ['Data Analytics', 'Consulting'] }
    ]
  },
  {
    company: 'Tellennium',
    location: 'Louisville, KY',
    title: 'Project Manager / Technical Services Specialist',
    dates: '2016 – 2019',
    bullets: [
      { text: 'Managed large-scale telecom projects including multi-site service disconnects, carrier dispositions, and enterprise phone system migrations.', tags: ['Project Management'] },
      { text: 'Coordinated circuit lifecycle management for WAN, PRI, SIP, and analog services — ordering, transfers of ownership, audits, optimization, and vendor/carrier communication.', tags: ['Project Management', 'Consulting'] },
      { text: 'Verified carrier invoices against contracts and initiated billing disputes, recovering credits and ensuring contracted rates were applied.', tags: ['Consulting', 'Data Analytics'] },
      { text: 'Administered deployments and configuration changes for 300+ devices using AirWatch MDM; provided Tier 1–2 support for wireline, wireless, and Avaya PBX systems.', tags: ['Project Management', 'Consulting'] }
    ]
  }
]

const volunteer = [
  {
    org: "з любов'ю (with love)",
    location: 'Louisville, KY / International',
    title: 'Co-Founder — Logistics & Operations',
    bullets: [
      { text: 'Co-founded an international humanitarian aid initiative delivering over 3 tons of supplies to Ukraine, leveraging global relationships to route goods to high-need areas.', tags: ['Project Management', 'Consulting'] }
    ]
  },
  {
    org: 'Louisville Grows',
    location: 'Louisville, KY',
    title: 'Data Dashboard Developer',
    bullets: [
      { text: 'Developed an internal data dashboard to track historical and current tree planting efforts, streamlining reporting for grant funding and directing future planting strategy.', tags: ['Data Analytics', 'Consulting'] }
    ]
  }
]

const skills = [
  // Software / Full Stack
  { name: 'Vue.js & React', tags: ['Software Developer'] },
  { name: 'JavaScript, HTML & CSS', tags: ['Software Developer'] },
  { name: 'Node.js & FastAPI', tags: ['Software Developer'] },
  { name: 'C# & .NET', tags: ['Software Developer'] },
  { name: 'REST APIs & WebSockets', tags: ['Software Developer', 'Data Analytics'] },
  { name: 'Docker & Containerization', tags: ['Software Developer', 'Project Management'] },
  { name: 'AWS, Azure & Cloud Deployment', tags: ['Software Developer', 'Project Management'] },
  { name: 'CI/CD & GitHub Actions', tags: ['Software Developer', 'Project Management'] },
  { name: 'QA Automation & Selenium', tags: ['Software Developer'] },
  { name: 'Technical SEO & Schema / JSON-LD', tags: ['Software Developer', 'Data Analytics'] },
  { name: 'Security — Cloudflare WAF, DNS Hardening', tags: ['Software Developer', 'Consulting'] },
  { name: 'UI/UX — Wireframing to Production', tags: ['Software Developer'] },
  // Data
  { name: 'Python, Pandas & NumPy', tags: ['Data Analytics', 'Software Developer'] },
  { name: 'SQL — MySQL, PostgreSQL, DuckDB', tags: ['Data Analytics', 'Software Developer'] },
  { name: 'BI Dashboards — Tableau, Streamlit, Chart.js', tags: ['Data Analytics'] },
  { name: 'Data Pipeline Engineering', tags: ['Data Analytics', 'Software Developer'] },
  { name: 'AI / LLM Integration & Prompt Engineering', tags: ['Data Analytics', 'Software Developer'] },
  { name: 'Automated Reporting & Email Delivery', tags: ['Data Analytics', 'Consulting'] },
  { name: 'Data Storytelling & Stakeholder Visualization', tags: ['Data Analytics', 'Consulting'] },
  // PM / Consulting
  { name: 'Agile, Scrum & Sprint Management', tags: ['Project Management'] },
  { name: 'Portfolio & Program Management', tags: ['Project Management', 'Consulting'] },
  { name: 'Client Discovery & MVP Scoping', tags: ['Consulting', 'Project Management'] },
  { name: 'Stakeholder Management & Executive Communication', tags: ['Consulting', 'Project Management'] },
  { name: 'Vendor Negotiation & Procurement', tags: ['Consulting', 'Project Management'] },
  { name: 'Budget Ownership & Cost Optimization', tags: ['Consulting', 'Project Management'] },
  { name: 'Curriculum Design & Technical Training', tags: ['Project Management', 'Consulting'] },
  { name: 'Influence Without Authority', tags: ['Consulting', 'Project Management'] }
]

//  COMPUTED PROPERTIES
const filteredJobs = computed(() => {
  return jobs.map(job => {
    return { ...job, bullets: job.bullets.filter(b => matchesFilter(b.tags)) }
  }).filter(job => job.bullets.length > 0)
})

const filteredVolunteer = computed(() => {
  return volunteer.map(v => {
    return { ...v, bullets: v.bullets.filter(b => matchesFilter(b.tags)) }
  }).filter(v => v.bullets.length > 0)
})

const filteredSkills = computed(() => {
  return skills.filter(skill => matchesFilter(skill.tags)).map(s => s.name)
})
</script>

<template>
  <div class="resume-container">

    <div class="filter-controls no-print">
      <p class="filter-label">Tailor this resume for:</p>
      <div class="button-group">
        <button
          v-for="cat in categories"
          :key="cat"
          :class="{ active: selectedCategory === cat }"
          @click="selectedCategory = cat"
        >
          {{ cat }}
        </button>
      </div>
      <button class="export-btn" @click="exportToPDF">
        <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" style="margin-right: 6px; vertical-align: text-bottom;"><path d="M21 15v4a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2v-4"></path><polyline points="7 10 12 15 17 10"></polyline><line x1="12" y1="15" x2="12" y2="3"></line></svg>
        Save as PDF
      </button>
    </div>

    <div class="resume-paper">

      <header>
        <DmLogo :centered="true" size="2.8rem" />
        <p class="contact-line">{{ contactInfo.location }} | P: {{ contactInfo.phone }} | {{ contactInfo.email }}</p>
      </header>

      <hr />

      <section>
        <h2>Education</h2>
        <div v-for="edu in education" :key="edu.degree" class="entry-header">
          <div>
            <strong>{{ edu.school }}</strong> — <em>{{ edu.location }}</em>
            <div class="subtitle">{{ edu.degree }}</div>
          </div>
          <div class="date">{{ edu.year }}</div>
        </div>
      </section>

      <section v-if="filteredJobs.length > 0">
        <h2>Work Experience</h2>
        <div v-for="job in filteredJobs" :key="job.company + job.title" class="job-block">
          <div class="entry-header">
            <div>
              <strong>{{ job.company }}</strong> — <em>{{ job.location }}</em>
              <div class="subtitle">{{ job.title }}</div>
            </div>
            <div class="date">{{ job.dates }}</div>
          </div>
          <ul>
            <li v-for="(bullet, index) in job.bullets" :key="index">
              {{ bullet.text }}
            </li>
          </ul>
        </div>
      </section>

      <section v-if="filteredVolunteer.length > 0">
        <h2>Volunteer & Community</h2>
        <div v-for="v in filteredVolunteer" :key="v.org" class="job-block">
          <div class="entry-header">
            <div>
              <strong>{{ v.org }}</strong> — <em>{{ v.location }}</em>
              <div class="subtitle">{{ v.title }}</div>
            </div>
          </div>
          <ul>
            <li v-for="(bullet, index) in v.bullets" :key="index">
              {{ bullet.text }}
            </li>
          </ul>
        </div>
      </section>

      <section v-if="filteredSkills.length > 0">
        <h2>Skills Focus ({{ selectedCategory }})</h2>
        <p class="skills-list">{{ filteredSkills.join(', ') }}</p>
      </section>

    </div>
  </div>
</template>

<style scoped>
.resume-container {
  font-family: 'Inter', -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Helvetica, Arial, sans-serif;
  color: #333;
  max-width: 900px;
  margin: 0 auto;
  padding: 20px;
}

.filter-controls {
  margin-bottom: 30px;
  text-align: center;
}

.filter-label {
  font-size: 0.9rem;
  color: #666;
  margin-bottom: 8px;
  text-transform: uppercase;
  letter-spacing: 1px;
}

.button-group {
  display: flex;
  justify-content: center;
  gap: 10px;
  flex-wrap: wrap;
  margin-bottom: 15px;
}

button {
  background: #f1f5f9;
  border: 1px solid #cbd5e1;
  padding: 8px 16px;
  border-radius: 20px;
  cursor: pointer;
  font-size: 0.9rem;
  transition: all 0.2s;
  color: #475569;
}

button:hover {
  background: #e2e8f0;
}

button.active {
  background: #2563eb;
  color: white;
  border-color: #2563eb;
}

.export-btn {
  background: #10b981;
  color: white;
  border-color: #059669;
  font-weight: 600;
}

.export-btn:hover {
  background: #059669;
}

.resume-paper {
  background: white;
  padding: 40px;
  border-radius: 8px;
  box-shadow: 0 4px 6px rgba(0,0,0,0.05);
  border: 1px solid #e2e8f0;
}

header {
  text-align: center;
  margin-bottom: 20px;
}

.contact-line {
  margin: 10px 0 0 0;
  color: #64748b;
  font-size: 0.95rem;
}

hr {
  border: none;
  border-top: 1px solid #cbd5e1;
  margin: 20px 0;
}

h2 {
  font-size: 1.2rem;
  color: #0f172a;
  text-transform: uppercase;
  letter-spacing: 1px;
  border-bottom: 2px solid #2563eb;
  padding-bottom: 4px;
  margin-top: 25px;
  margin-bottom: 15px;
}

.entry-header {
  display: flex;
  justify-content: space-between;
  align-items: baseline;
  margin-bottom: 5px;
}

.subtitle {
  font-weight: 600;
  color: #475569;
}

.date {
  font-weight: 500;
  color: #64748b;
  white-space: nowrap;
}

.job-block {
  margin-bottom: 20px;
}

ul {
  margin-top: 5px;
  padding-left: 20px;
  color: #334155;
}

li {
  margin-bottom: 5px;
  line-height: 1.5;
}

.skills-list {
  line-height: 1.6;
  color: #334155;
}

@media (max-width: 768px) {
  .resume-paper {
    padding: 20px 15px;
    border-radius: 0;
    border: none;
    box-shadow: none;
  }

  .button-group {
    gap: 8px;
    margin-bottom: 10px;
  }

  button {
    padding: 6px 12px;
    font-size: 0.85rem;
  }

  .export-btn {
    display: flex;
    width: 100%;
    justify-content: center;
    align-items: center;
    margin-top: 15px;
    padding: 12px;
  }

  .entry-header {
    flex-direction: column;
    align-items: flex-start;
    gap: 4px;
    margin-bottom: 10px;
  }

  .date {
    font-size: 0.9rem;
    color: #2563eb;
  }

  h2 {
    font-size: 1.1rem;
    margin-top: 20px;
  }
}

@media print {
  @page {
    margin: 0.5in;
  }

  body {
    background: white;
    -webkit-print-color-adjust: exact;
  }

  .resume-container {
    max-width: 100%;
    padding: 0;
    margin: 0;
  }

  .resume-paper {
    box-shadow: none;
    border: none;
    padding: 0;
  }

  .no-print {
    display: none !important;
  }

  h2 {
    page-break-after: avoid;
    break-after: avoid;
  }

  .job-block, .entry-header {
    page-break-inside: avoid;
    break-inside: avoid;
  }
}
</style>
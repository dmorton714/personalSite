<script setup>
import { ref, computed } from 'vue'
import DmLogo from './DmLogo.vue' // Adjust the path if necessary

//  FILTER STATE 
const categories = ['All', 'Data Analytics', 'Project Management', 'Consulting', 'Creative']
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
    degree: 'Political Science',
    year: '2010'
  },
  {
    school: 'Jefferson Community And Technical College',
    location: 'Louisville, KY',
    degree: 'Associates of Applied Science in Graphic Design; Minor in Web Design',
    year: '2013'
  }
]

const jobs = [
  {
    company: 'Code:You (Nonprofit coding bootcamp)',
    location: 'Louisville, KY',
    title: 'Technical Project Manager',
    dates: '2023 – Current',
    bullets: [
      { text: 'Manage and mentor graduates transitioning into the tech workforce; provide project-based learning opportunities to build portfolios and improve job readiness.', tags: ['Project Management', 'Consulting'] },
      { text: 'Partner with nonprofit organizations (up to 20 at a time) to identify and deliver technical solutions, overseeing end-to-end project scoping, development, and delivery.', tags: ['Project Management', 'Consulting'] },
      { text: 'Spearheaded curriculum development for C#, JavaScript, AI, AWS, and Python with a focus on industry relevance and learner outcomes; leveraged data-driven strategies to improve student retention and course completion by ~10%.', tags: ['Data Analytics', 'Creative', 'Project Management'] },
      { text: 'Recruit and coordinate volunteers to support student learning and program initiatives, cultivating a strong, mission-aligned community.', tags: ['Project Management', 'Consulting'] },
      { text: 'Collaborate on digital marketing and outreach strategies, contributing insights to improve engagement across web, email, and social media platforms.', tags: ['Creative', 'Data Analytics'] }
    ]
  },
  {
    company: 'Best One Tires',
    location: 'Louisville, KY',
    title: 'IT Manager',
    dates: '2021 – Current',
    bullets: [
      { text: 'Designed and implemented real-time Business Intelligence (BI) dashboards to track sales performance and forecast growth trends, enabling strategic inventory planning during the COVID-19 supply chain crisis; contributed to 15%+ business growth.', tags: ['Data Analytics'] },
      { text: 'Automated deployment and update processes using custom scripts in a Remote Monitoring & Management (RMM) platform, saving over 20 hours of manual IT labor monthly.', tags: ['Project Management', 'Consulting'] },
      { text: 'Led end-to-end cloud migration of a self-hosted SaaS (Maddenco), reducing annual costs by $20K and eliminating hardware, licensing, and network security overhead.', tags: ['Project Management', 'Consulting'] },
      { text: 'Orchestrated cellular migration of 200+ field devices to a new provider, cutting telecom costs by $12K/year and enhancing sales team productivity.', tags: ['Project Management'] },
      { text: 'Negotiated fiber connectivity contracts with ISPs, improving network speed and stability across multiple sites while reducing expenses by $5K annually.', tags: ['Consulting', 'Project Management'] },
      { text: 'Migrated on-premise SQL server to a cloud-hosted environment, modernizing infrastructure, enhancing scalability, and eliminating end-of-life systems and licensing costs.', tags: ['Data Analytics', 'Project Management'] },
      { text: 'Oversaw transition to hosted VoIP solution, streamlining telecom operations and saving $12K annually in third-party support and licensing fees.', tags: ['Project Management'] },
      { text: 'Documented and standardized all core IT and operational procedures, establishing repeatable best practices and improving cross-departmental efficiency.', tags: ['Project Management', 'Consulting'] },
      { text: 'Negotiated new credit card processing agreement, saving the company over $187K annually through a custom fee model based on transaction patterns.', tags: ['Consulting', 'Data Analytics'] }
    ]
  },
  {
    company: 'ADI (Resideo/Honeywell)',
    location: 'Louisville, KY',
    title: 'Technical Hardware Support Specialist',
    dates: '2019 – 2021',
    bullets: [
      { text: 'Contributed to the development and optimization of Salesforce and internal software systems, enabling cross-departmental BI reporting and real-time updates that enhanced sales and operational transparency.', tags: ['Data Analytics', 'Project Management'] },
      { text: 'Streamlined daily order processing workflows, reducing redundant tasks and improving visibility across teams; directly supported an increase in sales efficiency.', tags: ['Project Management', 'Consulting'] },
      { text: 'Created custom scripting solutions for hardware programming tasks, reducing manual labor by 20+ hours on large orders and doubling departmental capacity for client onboarding.', tags: ['Creative', 'Data Analytics', 'Project Management'] },
      { text: 'Programmed IP cameras, NVRs, and SQL-based systems to be pre-configured for plug-and-play deployment, improving customer experience and reducing post-sale support needs.', tags: ['Project Management'] }
    ]
  },
  {
    company: 'Tellennium',
    location: 'Louisville, KY',
    title: 'Project Manager / Technical Services Specialist',
    dates: '2016 – 2019',
    bullets: [
      { text: 'Supported the development and enhancement of an internal property ticketing system and TIMS software, improving issue tracking and operational visibility across telecom services.', tags: ['Project Management'] },
      { text: 'Provided Tier 1–2 technical support for wireline and wireless services, ensuring SLA compliance and rapid issue resolution.', tags: ['Consulting'] },
      { text: 'Managed large-scale telecom projects, including multi-site service disconnects due to facility closures, carrier dispositions, and enterprise phone system migrations.', tags: ['Project Management'] },
      { text: 'Coordinated circuit lifecycle management for WAN, PRI, SIP, and analog services, including ordering, transfers of ownership, audits, optimization, and vendor/carrier communication.', tags: ['Project Management'] },
      { text: 'Identified cost-reduction opportunities and proposed alternative telecom solutions, delivering ongoing month-to-month savings aligned with evolving contract and business needs.', tags: ['Data Analytics', 'Consulting'] }
    ]
  }
]

const projects = [
  {
    title: 'Louisville Foreclosure Dashboard',
    year: '2025',
    bullets: [
      { text: 'Built a Streamlit dashboard to visualize and analyze Foreclosures in Louisville KY.', tags: ['Data Analytics', 'Creative'] },
      { text: 'This was built to be a test assignment for students entering into the Code:You Pipeline.', tags: ['Project Management', 'Consulting'] },
      { text: 'Built with GoLang, Python, and CSS.', tags: ['Creative', 'Data Analytics'] }
    ]
  },
  {
    title: 'Code:You Sample Project Repository',
    year: '2025',
    bullets: [
      { text: 'Developed and maintained a dedicated repository to teach advanced, real-world software practices not fully covered in core bootcamp curriculum.', tags: ['Project Management', 'Creative'] },
      { text: 'Created modules on transforming Jupyter notebooks into production-ready Python code, introducing OOP concepts, writing unit tests, and applying optimization strategies.', tags: ['Data Analytics', 'Creative'] },
      { text: 'Designed break–fix exercises to improve students’ debugging skills and build confidence handling real-world production issues.', tags: ['Consulting', 'Project Management'] }
    ]
  }
]

const skills = [
  { name: 'Project Management', tags: ['Project Management', 'Consulting'] },
  { name: 'Scrum & Agile', tags: ['Project Management'] },
  { name: 'Python & SQL', tags: ['Data Analytics', 'Creative'] },
  { name: 'HTML/CSS & Vue', tags: ['Creative'] },
  { name: 'Golang & Rest APIs', tags: ['Creative', 'Data Analytics'] },
  { name: 'Data Storytelling', tags: ['Data Analytics', 'Consulting'] },
  { name: 'Stakeholder Management', tags: ['Consulting', 'Project Management'] },
  { name: 'Influence Without Authority', tags: ['Consulting', 'Project Management'] },
  { name: 'GIS & R', tags: ['Data Analytics'] }
]

//  COMPUTED PROPERTIES 
const filteredJobs = computed(() => {
  return jobs.map(job => {
    return { ...job, bullets: job.bullets.filter(b => matchesFilter(b.tags)) }
  }).filter(job => job.bullets.length > 0)
})

const filteredProjects = computed(() => {
  return projects.map(proj => {
    return { ...proj, bullets: proj.bullets.filter(b => matchesFilter(b.tags)) }
  }).filter(proj => proj.bullets.length > 0)
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

      <section v-if="filteredProjects.length > 0">
        <h2>Projects</h2>
        <div v-for="proj in filteredProjects" :key="proj.title" class="job-block">
          <div class="entry-header">
            <strong>{{ proj.title }}</strong>
            <div class="date">{{ proj.year }}</div>
          </div>
          <ul>
            <li v-for="(bullet, index) in proj.bullets" :key="index">
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
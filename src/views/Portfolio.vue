<template>
  <div class="portfolio" :class="{ scrolled: isScrolled }">

    <!-- NAV -->
    <nav class="nav">
      <span class="nav-logo">J<span class="dot">.</span></span>
      <ul class="nav-links">
        <li><a href="#about" @click.prevent="scrollTo('about')">About</a></li>
        <li><a href="#skills" @click.prevent="scrollTo('skills')">Skills</a></li>
        <li><a href="#projects" @click.prevent="scrollTo('projects')">Projects</a></li>
        <li><a href="#contact" @click.prevent="scrollTo('contact')">Contact</a></li>
      </ul>
      <a href="#contact" @click.prevent="scrollTo('contact')" class="nav-cta">Hire Me</a>
    </nav>

    <!-- HERO -->
    <section class="hero" id="hero">
      <div class="hero-bg">
        <div class="grid-overlay"></div>
        <div class="glow glow-1"></div>
        <div class="glow glow-2"></div>
      </div>

      <div class="hero-inner">
        <div class="hero-text" :class="{ visible: heroVisible }">
          <div class="badge">

          <h1 class="hero-title">
            Hi, I'm<br>
            <span class="name-gradient">Josue</span>
          </h1>

          <p class="hero-role">Vue.js Developer <span class="sep">·</span> UI Designer</p>

          <p class="hero-desc">
            Crafting modern, responsive web experiences with
            Vue.js, JavaScript, and a sharp eye for design.
          </p>

          <div class="hero-actions">
            <button class="btn-primary" @click="scrollTo('projects')">
              View Projects
              <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M5 12h14M12 5l7 7-7 7"/></svg>
            </button>
            <button class="btn-ghost" @click="scrollTo('contact')">Contact Me</button>
          </div>
        </div>

        <div class="hero-image" :class="{ visible: heroVisible }">
          <div class="img-frame">
            <img src="../assets/josue.png" alt="Josue" />
            <div class="img-border"></div>
          </div>
          <div class="float-card card-exp">
            <span class="fc-num">2+</span>
            <span class="fc-label">Years</span>
          </div>
          <div class="float-card card-proj">
            <span class="fc-num">10+</span>
            <span class="fc-label">Projects</span>
          </div>
        </div>
      </div>

      <div class="scroll-hint" @click="scrollTo('about')">
        <div class="scroll-mouse"><div class="scroll-wheel"></div></div>
        <span>Scroll</span>
      </div>
    </section>

    <!-- STATS -->
    <section class="stats-bar">
      <div class="stats-inner">
        <div
          v-for="(stat, i) in stats"
          :key="i"
          class="stat-item"
          :class="{ visible: statsVisible }"
          :style="{ transitionDelay: `${i * 120}ms` }"
        >
          <span class="stat-num">{{ stat.num }}</span>
          <span class="stat-label">{{ stat.label }}</span>
        </div>
      </div>
    </section>

    <!-- ABOUT -->
    <section class="section about-section" id="about">
      <div class="section-inner">
        <div class="section-label">WHO I AM</div>
        <h2 class="section-title">About Me</h2>
        <div class="about-grid">
          <div class="about-text" :class="{ visible: aboutVisible }">
            <p>
              I'm a passionate frontend developer based in Rwanda, focused on
              building modern, responsive websites that solve real-world problems.
            </p>
            <p>
              My approach combines clean code with beautiful interfaces — every
              project I build prioritizes both performance and the user experience.
            </p>
            <p>
              When I'm not coding, I'm exploring new design trends and pushing
              the boundaries of what's possible on the web.
            </p>
            <div class="about-tags">
              <span v-for="t in aboutTags" :key="t" class="about-tag">{{ t }}</span>
            </div>
          </div>
          <div class="about-cards" :class="{ visible: aboutVisible }">
            <div
              v-for="(card, i) in aboutCards"
              :key="i"
              class="about-card"
              :style="{ transitionDelay: `${i * 80}ms` }"
            >
              <div class="ac-icon" v-html="card.icon"></div>
              <h4>{{ card.title }}</h4>
              <p>{{ card.desc }}</p>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- SKILLS -->
    <section class="section skills-section" id="skills">
      <div class="section-inner">
        <div class="section-label">WHAT I KNOW</div>
        <h2 class="section-title">Skills</h2>
        <div class="skills-grid">
          <div
            v-for="(skill, i) in skills"
            :key="skill.name"
            class="skill-card"
            :class="{ visible: skillsVisible }"
            :style="{ transitionDelay: `${i * 60}ms` }"
          >
            <div class="skill-bar-bg">
              <div
                class="skill-bar-fill"
                :style="{ width: skillsVisible ? skill.level + '%' : '0%', transitionDelay: `${i * 60 + 300}ms` }"
              ></div>
            </div>
            <div class="skill-info">
              <span class="skill-name">{{ skill.name }}</span>
              <span class="skill-pct">{{ skill.level }}%</span>
            </div>
          </div>
        </div>
        <div class="tools-row">
          <span
            v-for="(tool, i) in tools"
            :key="tool"
            class="tool-pill"
            :class="{ visible: skillsVisible }"
            :style="{ transitionDelay: `${i * 50 + 400}ms` }"
          >{{ tool }}</span>
        </div>
      </div>
    </section>

    <!-- PROJECTS -->
    <section class="section projects-section" id="projects">
      <div class="section-inner">
        <div class="section-label">WHAT I'VE BUILT</div>
        <h2 class="section-title">Featured Projects</h2>
        <div class="projects-grid">
          <div
            v-for="(project, i) in projects"
            :key="project.title"
            class="project-card"
            :class="{ visible: projectsVisible }"
            :style="{ transitionDelay: `${i * 100}ms` }"
            @mouseenter="activeProject = i"
            @mouseleave="activeProject = null"
          >
            <div class="pc-image">
              <img :src="project.img" :alt="project.title" />
              <div class="pc-overlay" :class="{ active: activeProject === i }">
                <button class="pc-btn">View Project</button>
              </div>
            </div>
            <div class="pc-body">
              <div class="pc-tags">
                <span v-for="tag in project.tags" :key="tag" class="pc-tag">{{ tag }}</span>
              </div>
              <h3>{{ project.title }}</h3>
              <p>{{ project.desc }}</p>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- CONTACT -->
    <section class="section contact-section" id="contact">
      <div class="section-inner">
        <div class="contact-inner">
          <div class="contact-left" :class="{ visible: contactVisible }">
            <div class="section-label">GET IN TOUCH</div>
            <h2 class="section-title">Let's Work<br>Together</h2>
            <p class="contact-sub">
              Have a project in mind? I'd love to hear about it.
              Send me a message and let's make something great.
            </p>
            <div class="contact-info">
              <div class="ci-item" v-for="item in contactInfo" :key="item.label">
                <div class="ci-icon" v-html="item.icon"></div>
                <div>
                  <span class="ci-label">{{ item.label }}</span>
                  <span class="ci-value">{{ item.value }}</span>
                </div>
              </div>
            </div>
          </div>

          <form class="contact-form" :class="{ visible: contactVisible }" @submit.prevent="submitForm">
            <div class="form-row">
              <div class="form-group">
                <label>Name</label>
                <input v-model="form.name" type="text" placeholder="Your name" required />
              </div>
              <div class="form-group">
                <label>Email</label>
                <input v-model="form.email" type="email" placeholder="your@email.com" required />
              </div>
            </div>
            <div class="form-group">
              <label>Subject</label>
              <input v-model="form.subject" type="text" placeholder="What's this about?" />
            </div>
            <div class="form-group">
              <label>Message</label>
              <textarea v-model="form.message" rows="5" placeholder="Tell me about your project..." required></textarea>
            </div>
            <button type="submit" class="btn-primary form-submit" :class="{ sent: formSent }">
              <span v-if="!formSent">
                Send Message
                <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M22 2L11 13M22 2l-7 20-4-9-9-4 20-7z"/></svg>
              </span>
              <span v-else>Sent! ✓</span>
            </button>
          </form>
        </div>
      </div>
    </section>

    <!-- FOOTER -->
    <footer class="footer">
      <div class="footer-inner">
        <span class="nav-logo">J<span class="dot">.</span></span>
        <p>Frontend Developer · Vue.js · UI Designer</p>
        <p class="footer-copy">© 2026 Josue. All rights reserved.</p>
      </div>
    </footer>

  </div>
</template>

<script>
export default {
  name: 'Portfolio',
  data() {
    return {
      isScrolled: false,
      heroVisible: false,
      statsVisible: false,
      aboutVisible: false,
      skillsVisible: false,
      projectsVisible: false,
      contactVisible: false,
      activeProject: null,
      formSent: false,
      form: { name: '', email: '', subject: '', message: '' },

      stats: [
        { num: '10+', label: 'Projects Completed' },
        { num: '5+',  label: 'Web Applications' },
        { num: '2+',  label: 'Years of Learning' },
        { num: '100%', label: 'Passion for Code' },
      ],

      aboutTags: ['Problem Solver', 'Detail-Oriented', 'Fast Learner', 'Team Player'],

      aboutCards: [
        {
          icon: '<svg width="22" height="22" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.8"><polyline points="16 18 22 12 16 6"/><polyline points="8 6 2 12 8 18"/></svg>',
          title: 'Frontend Dev',
          desc: 'Building responsive, accessible UIs with Vue.js and modern CSS.',
        },
        {
          icon: '<svg width="22" height="22" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.8"><circle cx="12" cy="12" r="3"/><path d="M19.07 4.93a10 10 0 010 14.14"/><path d="M4.93 4.93a10 10 0 000 14.14"/></svg>',
          title: 'UI Designer',
          desc: 'Crafting beautiful, intuitive interfaces users actually enjoy.',
        },
        {
          icon: '<svg width="22" height="22" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.8"><path d="M12 2L2 7l10 5 10-5-10-5zM2 17l10 5 10-5M2 12l10 5 10-5"/></svg>',
          title: 'Web Apps',
          desc: 'Delivering full-featured apps with clean architecture and great UX.',
        },
      ],

      skills: [
        { name: 'Vue.js',       level: 88 },
        { name: 'JavaScript',   level: 85 },
        { name: 'HTML5 & CSS3', level: 92 },
        { name: 'Tailwind CSS', level: 80 },
        { name: 'UI Design',    level: 75 },
        { name: 'GitHub',       level: 78 },
      ],

      tools: ['Vue Router', 'Pinia', 'Vite', 'Figma', 'Git', 'REST APIs', 'Responsive Design', 'Netlify'],

      projects: [
        {
          title: 'AkaziHub',
          desc: 'Platform connecting job seekers, service providers and customers in one seamless marketplace.',
          img: 'https://images.unsplash.com/photo-1498050108023-c5249f4df085?w=800',
          tags: ['Vue.js', 'Platform', 'UX'],
        },
        {
          title: 'Rwanda Tourism',
          desc: 'Tourism website showcasing Rwanda\'s stunning attractions, culture and hospitality.',
          img: 'https://images.unsplash.com/photo-1469474968028-56623f02e42e?w=800',
          tags: ['Vue.js', 'Tourism', 'Design'],
        },
        {
          title: 'School Portal',
          desc: 'Vue Router application with multiple pages, student dashboards and responsive design.',
          img: 'https://images.unsplash.com/photo-1516321318423-f06f85e504b3?w=800',
          tags: ['Vue Router', 'Dashboard', 'Education'],
        },
      ],

      contactInfo: [
        {
          icon: '<svg width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M4 4h16c1.1 0 2 .9 2 2v12c0 1.1-.9 2-2 2H4c-1.1 0-2-.9-2-2V6c0-1.1.9-2 2-2z"/><polyline points="22,6 12,13 2,6"/></svg>',
          label: 'Email',
          value: 'josue@example.com',
        },
        {
          icon: '<svg width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M21 10c0 7-9 13-9 13s-9-6-9-13a9 9 0 0118 0z"/><circle cx="12" cy="10" r="3"/></svg>',
          label: 'Location',
          value: 'Kigali, Rwanda',
        },
      ],
    }
  },

  mounted() {
    window.addEventListener('scroll', this.onScroll)
    this.setupObservers()
    setTimeout(() => { this.heroVisible = true }, 100)
  },

  beforeUnmount() {
    window.removeEventListener('scroll', this.onScroll)
  },

  methods: {
    onScroll() {
      this.isScrolled = window.scrollY > 60
    },

    scrollTo(id) {
      const el = document.getElementById(id)
      if (el) el.scrollIntoView({ behavior: 'smooth' })
    },

    setupObservers() {
      const observe = (selector, prop, threshold = 0.2) => {
        const el = document.querySelector(selector)
        if (!el) return
        const obs = new IntersectionObserver(
          ([entry]) => { if (entry.isIntersecting) { this[prop] = true; obs.disconnect() } },
          { threshold }
        )
        obs.observe(el)
      }
      observe('.stats-bar',       'statsVisible',   0.3)
      observe('.about-section',   'aboutVisible',   0.2)
      observe('.skills-section',  'skillsVisible',  0.2)
      observe('.projects-section','projectsVisible',0.1)
      observe('.contact-section', 'contactVisible', 0.15)
    },

    submitForm() {
      this.formSent = true
      setTimeout(() => {
        this.formSent = false
        this.form = { name: '', email: '', subject: '', message: '' }
      }, 3000)
    },
  },
}
</script>

<style scoped>
/* ── TOKENS ── */
:root {
  --bg:        #0a0a0f;
  --bg2:       #0f0f18;
  --bg3:       #14141f;
  --surface:   #1a1a28;
  --surf2:     #20202f;
  --border:    rgba(255,255,255,0.07);
  --border2:   rgba(255,255,255,0.12);
  --text:      #f0f0f8;
  --muted:     #8888aa;
  --accent:    #6c63ff;
  --accent2:   #a78bfa;
  --accent3:   #38bdf8;
  --green:     #34d399;
  --grad:      linear-gradient(135deg, #6c63ff, #a78bfa, #38bdf8);
  --radius:    16px;
  --radius-sm: 10px;
  --nav-h:     72px;
  --font:      'Syne', sans-serif;
  --mono:      'JetBrains Mono', monospace;
}

/* ── RESET & BASE ── */
* { margin: 0; padding: 0; box-sizing: border-box; }

.portfolio {
  background: var(--bg);
  color: var(--text);
  font-family: var(--font), 'Segoe UI', sans-serif;
  overflow-x: hidden;
}

a { text-decoration: none; color: inherit; }

/* ── NAV ── */
.nav {
  position: fixed;
  top: 0; left: 0; right: 0;
  z-index: 100;
  display: flex;
  align-items: center;
  padding: 0 7%;
  height: var(--nav-h);
  transition: background 0.4s, backdrop-filter 0.4s, border-bottom 0.4s;
}

.scrolled .nav {
  background: rgba(10,10,15,0.85);
  backdrop-filter: blur(16px);
  border-bottom: 1px solid var(--border);
}

.nav-logo {
  font-size: 1.8rem;
  font-weight: 800;
  letter-spacing: -1px;
  margin-right: auto;
}

.dot { color: var(--accent); }

.nav-links {
  display: flex;
  gap: 36px;
  list-style: none;
}

.nav-links a {
  font-size: 0.9rem;
  color: var(--muted);
  font-weight: 500;
  letter-spacing: 0.5px;
  transition: color 0.2s;
}

.nav-links a:hover { color: var(--text); }

.nav-cta {
  margin-left: 36px;
  background: var(--accent);
  color: #fff;
  padding: 10px 24px;
  border-radius: 50px;
  font-size: 0.9rem;
  font-weight: 600;
  transition: opacity 0.2s, transform 0.2s;
}

.nav-cta:hover { opacity: 0.85; transform: translateY(-1px); }

/* ── HERO ── */
.hero {
  position: relative;
  min-height: 100vh;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  padding: var(--nav-h) 7% 80px;
  overflow: hidden;
}

.hero-bg {
  position: absolute;
  inset: 0;
  pointer-events: none;
}

.grid-overlay {
  position: absolute;
  inset: 0;
  background-image:
    linear-gradient(rgba(108,99,255,0.05) 1px, transparent 1px),
    linear-gradient(90deg, rgba(108,99,255,0.05) 1px, transparent 1px);
  background-size: 60px 60px;
}

.glow {
  position: absolute;
  border-radius: 50%;
  filter: blur(120px);
  opacity: 0.25;
}

.glow-1 {
  width: 600px; height: 600px;
  top: -100px; left: -100px;
  background: var(--accent);
}

.glow-2 {
  width: 400px; height: 400px;
  bottom: -100px; right: 5%;
  background: var(--accent3);
  opacity: 0.15;
}

.hero-inner {
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 80px;
  width: 100%;
  max-width: 1200px;
  z-index: 1;
}

/* hero text */
.hero-text {
  flex: 1;
  opacity: 0;
  transform: translateY(30px);
  transition: opacity 0.8s ease, transform 0.8s ease;
}

.hero-text.visible { opacity: 1; transform: translateY(0); }

.badge {
  display: inline-flex;
  align-items: center;
  gap: 8px;
  background: rgba(52,211,153,0.1);
  border: 1px solid rgba(52,211,153,0.3);
  color: var(--green);
  padding: 8px 18px;
  border-radius: 50px;
  font-size: 0.82rem;
  font-weight: 600;
  letter-spacing: 0.5px;
  margin-bottom: 28px;
}

.badge-dot {
  width: 8px; height: 8px;
  background: var(--green);
  border-radius: 50%;
  animation: pulse 2s infinite;
}

@keyframes pulse {
  0%, 100% { opacity: 1; }
  50%       { opacity: 0.3; }
}

.hero-title {
  font-size: clamp(3rem, 6vw, 5.5rem);
  font-weight: 800;
  line-height: 1.05;
  letter-spacing: -2px;
  margin-bottom: 20px;
}

.name-gradient {
  background: var(--grad);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
}

.hero-role {
  font-size: 1.1rem;
  color: var(--muted);
  font-weight: 500;
  margin-bottom: 20px;
  letter-spacing: 0.5px;
}

.sep { margin: 0 10px; color: var(--accent); }

.hero-desc {
  font-size: 1rem;
  color: var(--muted);
  line-height: 1.8;
  max-width: 480px;
  margin-bottom: 40px;
}

.hero-actions {
  display: flex;
  gap: 16px;
  flex-wrap: wrap;
}

/* buttons */
.btn-primary {
  display: inline-flex;
  align-items: center;
  gap: 10px;
  background: var(--accent);
  color: #fff;
  border: none;
  padding: 15px 32px;
  border-radius: 50px;
  font-size: 0.95rem;
  font-weight: 600;
  font-family: inherit;
  cursor: pointer;
  transition: transform 0.25s, opacity 0.25s, background 0.25s;
}

.btn-primary:hover { transform: translateY(-3px); opacity: 0.88; }

.btn-ghost {
  background: transparent;
  color: var(--text);
  border: 1.5px solid var(--border2);
  padding: 15px 32px;
  border-radius: 50px;
  font-size: 0.95rem;
  font-weight: 600;
  font-family: inherit;
  cursor: pointer;
  transition: border-color 0.2s, background 0.2s;
}

.btn-ghost:hover { border-color: var(--accent); background: rgba(108,99,255,0.08); }

/* hero image */
.hero-image {
  position: relative;
  flex-shrink: 0;
  opacity: 0;
  transform: translateX(30px);
  transition: opacity 0.9s 0.2s ease, transform 0.9s 0.2s ease;
}

.hero-image.visible { opacity: 1; transform: translateX(0); }

.img-frame {
  position: relative;
  width: 360px;
  height: 450px;
}

.img-frame img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  border-radius: 24px;
  display: block;
  position: relative;
  z-index: 1;
}

.img-border {
  position: absolute;
  inset: -3px;
  border-radius: 26px;
  background: var(--grad);
  z-index: 0;
  opacity: 0.7;
}

.float-card {
  position: absolute;
  background: var(--surface);
  border: 1px solid var(--border2);
  border-radius: var(--radius-sm);
  padding: 14px 20px;
  display: flex;
  flex-direction: column;
  align-items: center;
  backdrop-filter: blur(10px);
  z-index: 2;
}

.card-exp  { bottom: 30px; left: -60px; }
.card-proj { top: 40px; right: -55px; }

.fc-num {
  font-size: 1.6rem;
  font-weight: 800;
  background: var(--grad);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
  line-height: 1;
}

.fc-label {
  font-size: 0.72rem;
  color: var(--muted);
  font-weight: 600;
  letter-spacing: 0.5px;
  margin-top: 2px;
}

/* scroll hint */
.scroll-hint {
  position: absolute;
  bottom: 32px;
  left: 50%;
  transform: translateX(-50%);
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 8px;
  cursor: pointer;
  opacity: 0.5;
  transition: opacity 0.2s;
  z-index: 1;
}

.scroll-hint:hover { opacity: 1; }
.scroll-hint span { font-size: 0.72rem; letter-spacing: 2px; color: var(--muted); }

.scroll-mouse {
  width: 24px; height: 38px;
  border: 2px solid var(--muted);
  border-radius: 12px;
  display: flex;
  justify-content: center;
  padding-top: 6px;
}

.scroll-wheel {
  width: 4px; height: 8px;
  background: var(--muted);
  border-radius: 2px;
  animation: scroll-anim 2s infinite;
}

@keyframes scroll-anim {
  0%   { transform: translateY(0); opacity: 1; }
  100% { transform: translateY(10px); opacity: 0; }
}

/* ── STATS BAR ── */
.stats-bar {
  background: var(--bg2);
  border-top: 1px solid var(--border);
  border-bottom: 1px solid var(--border);
  padding: 48px 7%;
}

.stats-inner {
  max-width: 1200px;
  margin: auto;
  display: flex;
  justify-content: space-around;
  flex-wrap: wrap;
  gap: 30px;
}

.stat-item {
  text-align: center;
  opacity: 0;
  transform: translateY(20px);
  transition: opacity 0.6s, transform 0.6s;
}

.stat-item.visible { opacity: 1; transform: translateY(0); }

.stat-num {
  display: block;
  font-size: 3rem;
  font-weight: 800;
  letter-spacing: -1px;
  background: var(--grad);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
  line-height: 1;
}

.stat-label {
  display: block;
  font-size: 0.85rem;
  color: var(--muted);
  font-weight: 500;
  margin-top: 6px;
  letter-spacing: 0.5px;
}

/* ── SECTIONS ── */
.section { padding: 110px 7%; }
.section-inner { max-width: 1200px; margin: auto; }

.section-label {
  font-size: 0.72rem;
  font-weight: 700;
  letter-spacing: 3px;
  color: var(--accent);
  margin-bottom: 16px;
}

.section-title {
  font-size: clamp(2rem, 4vw, 3rem);
  font-weight: 800;
  letter-spacing: -1px;
  margin-bottom: 56px;
  line-height: 1.1;
}

/* ── ABOUT ── */
.about-section { background: var(--bg); }

.about-grid {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 70px;
  align-items: start;
}

.about-text {
  opacity: 0;
  transform: translateX(-30px);
  transition: opacity 0.8s, transform 0.8s;
}

.about-text.visible { opacity: 1; transform: translateX(0); }

.about-text p {
  color: var(--muted);
  line-height: 1.9;
  font-size: 1rem;
  margin-bottom: 20px;
}

.about-tags {
  display: flex;
  flex-wrap: wrap;
  gap: 10px;
  margin-top: 28px;
}

.about-tag {
  background: rgba(108,99,255,0.12);
  border: 1px solid rgba(108,99,255,0.25);
  color: var(--accent2);
  padding: 8px 18px;
  border-radius: 50px;
  font-size: 0.82rem;
  font-weight: 600;
}

.about-cards {
  display: flex;
  flex-direction: column;
  gap: 20px;
  opacity: 0;
  transform: translateX(30px);
  transition: opacity 0.8s 0.2s, transform 0.8s 0.2s;
}

.about-cards.visible { opacity: 1; transform: translateX(0); }

.about-card {
  background: var(--surface);
  border: 1px solid var(--border);
  border-radius: var(--radius);
  padding: 26px;
  display: flex;
  gap: 18px;
  align-items: flex-start;
  transition: border-color 0.3s, transform 0.3s;
}

.about-card:hover {
  border-color: var(--accent);
  transform: translateX(6px);
}

.ac-icon {
  width: 44px; height: 44px;
  background: rgba(108,99,255,0.12);
  border-radius: 10px;
  display: flex;
  align-items: center;
  justify-content: center;
  color: var(--accent2);
  flex-shrink: 0;
}

.about-card h4 {
  font-size: 1rem;
  font-weight: 700;
  margin-bottom: 6px;
}

.about-card p {
  font-size: 0.88rem;
  color: var(--muted);
  line-height: 1.6;
}

/* ── SKILLS ── */
.skills-section { background: var(--bg2); }

.skills-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(340px, 1fr));
  gap: 24px;
  margin-bottom: 48px;
}

.skill-card {
  opacity: 0;
  transform: translateY(20px);
  transition: opacity 0.6s, transform 0.6s;
}

.skill-card.visible { opacity: 1; transform: translateY(0); }

.skill-info {
  display: flex;
  justify-content: space-between;
  margin-bottom: 10px;
}

.skill-name { font-size: 0.9rem; font-weight: 600; }
.skill-pct  { font-size: 0.82rem; color: var(--accent2); font-weight: 600; }

.skill-bar-bg {
  height: 6px;
  background: var(--surface);
  border-radius: 3px;
  overflow: hidden;
}

.skill-bar-fill {
  height: 100%;
  background: var(--grad);
  border-radius: 3px;
  width: 0;
  transition: width 1s cubic-bezier(0.4, 0, 0.2, 1);
}

.tools-row {
  display: flex;
  flex-wrap: wrap;
  gap: 12px;
}

.tool-pill {
  background: var(--bg3);
  border: 1px solid var(--border2);
  padding: 10px 20px;
  border-radius: 50px;
  font-size: 0.82rem;
  font-weight: 600;
  color: var(--muted);
  opacity: 0;
  transform: translateY(10px);
  transition: opacity 0.5s, transform 0.5s, color 0.2s, border-color 0.2s;
}

.tool-pill.visible { opacity: 1; transform: translateY(0); }
.tool-pill:hover { color: var(--text); border-color: var(--accent); }

/* ── PROJECTS ── */
.projects-section { background: var(--bg); }

.projects-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(320px, 1fr));
  gap: 28px;
}

.project-card {
  background: var(--surface);
  border: 1px solid var(--border);
  border-radius: var(--radius);
  overflow: hidden;
  opacity: 0;
  transform: translateY(30px);
  transition: opacity 0.6s, transform 0.6s, border-color 0.3s;
}

.project-card.visible  { opacity: 1; transform: translateY(0); }
.project-card:hover    { border-color: var(--accent); }

.pc-image {
  position: relative;
  height: 220px;
  overflow: hidden;
}

.pc-image img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  transition: transform 0.5s;
  display: block;
}

.project-card:hover .pc-image img { transform: scale(1.06); }

.pc-overlay {
  position: absolute;
  inset: 0;
  background: rgba(10,10,15,0.75);
  display: flex;
  align-items: center;
  justify-content: center;
  opacity: 0;
  transition: opacity 0.3s;
}

.pc-overlay.active { opacity: 1; }

.pc-btn {
  background: var(--accent);
  color: #fff;
  border: none;
  padding: 12px 28px;
  border-radius: 50px;
  font-size: 0.9rem;
  font-weight: 600;
  font-family: inherit;
  cursor: pointer;
  transform: translateY(10px);
  transition: transform 0.3s;
}

.pc-overlay.active .pc-btn { transform: translateY(0); }

.pc-body { padding: 24px; }

.pc-tags {
  display: flex;
  gap: 8px;
  flex-wrap: wrap;
  margin-bottom: 14px;
}

.pc-tag {
  background: rgba(108,99,255,0.12);
  color: var(--accent2);
  padding: 4px 12px;
  border-radius: 50px;
  font-size: 0.72rem;
  font-weight: 700;
  letter-spacing: 0.5px;
}

.pc-body h3 {
  font-size: 1.2rem;
  font-weight: 700;
  margin-bottom: 8px;
}

.pc-body p {
  font-size: 0.88rem;
  color: var(--muted);
  line-height: 1.7;
}

/* ── CONTACT ── */
.contact-section { background: var(--bg2); }

.contact-inner {
  display: grid;
  grid-template-columns: 1fr 1.4fr;
  gap: 80px;
  align-items: start;
}

.contact-left {
  opacity: 0;
  transform: translateX(-30px);
  transition: opacity 0.8s, transform 0.8s;
}

.contact-left.visible { opacity: 1; transform: translateX(0); }

.contact-sub {
  color: var(--muted);
  line-height: 1.8;
  margin-bottom: 40px;
  margin-top: -30px;
}

.contact-info { display: flex; flex-direction: column; gap: 20px; }

.ci-item {
  display: flex;
  align-items: center;
  gap: 16px;
}

.ci-icon {
  width: 40px; height: 40px;
  background: rgba(108,99,255,0.12);
  border-radius: 10px;
  display: flex;
  align-items: center;
  justify-content: center;
  color: var(--accent2);
  flex-shrink: 0;
}

.ci-label {
  display: block;
  font-size: 0.72rem;
  color: var(--muted);
  font-weight: 600;
  letter-spacing: 0.5px;
  margin-bottom: 2px;
}

.ci-value {
  display: block;
  font-size: 0.95rem;
  font-weight: 600;
}

/* form */
.contact-form {
  background: var(--surface);
  border: 1px solid var(--border);
  border-radius: var(--radius);
  padding: 40px;
  opacity: 0;
  transform: translateX(30px);
  transition: opacity 0.8s 0.2s, transform 0.8s 0.2s;
}

.contact-form.visible { opacity: 1; transform: translateX(0); }

.form-row {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 16px;
}

.form-group { margin-bottom: 20px; }

.form-group label {
  display: block;
  font-size: 0.8rem;
  font-weight: 700;
  letter-spacing: 0.5px;
  color: var(--muted);
  margin-bottom: 8px;
}

.form-group input,
.form-group textarea {
  width: 100%;
  background: var(--bg);
  border: 1px solid var(--border2);
  border-radius: var(--radius-sm);
  padding: 13px 16px;
  color: var(--text);
  font-family: inherit;
  font-size: 0.92rem;
  transition: border-color 0.2s;
  outline: none;
  resize: vertical;
}

.form-group input:focus,
.form-group textarea:focus {
  border-color: var(--accent);
}

.form-group input::placeholder,
.form-group textarea::placeholder { color: rgba(136,136,170,0.5); }

.form-submit { width: 100%; justify-content: center; border-radius: var(--radius-sm); }
.form-submit.sent { background: var(--green); }

/* ── FOOTER ── */
.footer {
  background: var(--bg);
  border-top: 1px solid var(--border);
  padding: 48px 7%;
}

.footer-inner {
  max-width: 1200px;
  margin: auto;
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 12px;
  text-align: center;
}

.footer-inner p { font-size: 0.88rem; color: var(--muted); }
.footer-copy { font-size: 0.78rem !important; opacity: 0.5; }

/* ── RESPONSIVE ── */
@media (max-width: 960px) {
  .hero-inner { flex-direction: column-reverse; text-align: center; gap: 50px; }
  .hero-text   { align-items: center; display: flex; flex-direction: column; }
  .hero-desc   { max-width: 100%; }
  .img-frame   { width: 280px; height: 340px; }
  .card-exp    { left: -30px; }
  .card-proj   { right: -30px; }
  .about-grid  { grid-template-columns: 1fr; gap: 40px; }
  .contact-inner { grid-template-columns: 1fr; gap: 40px; }
}

@media (max-width: 640px) {
  .nav-links { display: none; }
  .section { padding: 80px 5%; }
  .hero { padding-left: 5%; padding-right: 5%; }
  .stats-bar { padding: 40px 5%; }
  .form-row { grid-template-columns: 1fr; }
  .contact-form { padding: 24px; }
  .float-card { display: none; }
  .img-frame { width: 240px; height: 290px; }
}
</style>
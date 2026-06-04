<template>
  <div class="portfolio" :class="{ scrolled: isScrolled, light: isLight }">

    <!-- NAV -->
    <nav class="nav">
      <span class="nav-logo">J<span class="dot">.</span></span>
      <ul class="nav-links" :class="{ open: mobileMenuOpen }">
        <li><a href="#about"    @click.prevent="navTo('about')">About</a></li>
        <li><a href="#skills"   @click.prevent="navTo('skills')">Skills</a></li>
        <li><a href="#projects" @click.prevent="navTo('projects')">Projects</a></li>
        <li><a href="#contact"  @click.prevent="navTo('contact')">Contact</a></li>
      </ul>
      <div class="nav-right">
        <!-- Dark / Light toggle -->
        <button class="theme-toggle" @click="isLight = !isLight" :title="isLight ? 'Dark mode' : 'Light mode'">
          <span v-if="!isLight">
            <svg width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
              <circle cx="12" cy="12" r="5"/><line x1="12" y1="1" x2="12" y2="3"/>
              <line x1="12" y1="21" x2="12" y2="23"/><line x1="4.22" y1="4.22" x2="5.64" y2="5.64"/>
              <line x1="18.36" y1="18.36" x2="19.78" y2="19.78"/><line x1="1" y1="12" x2="3" y2="12"/>
              <line x1="21" y1="12" x2="23" y2="12"/><line x1="4.22" y1="19.78" x2="5.64" y2="18.36"/>
              <line x1="18.36" y1="5.64" x2="19.78" y2="4.22"/>
            </svg>
          </span>
          <span v-else>
            <svg width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
              <path d="M21 12.79A9 9 0 1111.21 3 7 7 0 0021 12.79z"/>
            </svg>
          </span>
        </button>
        <a href="#contact" @click.prevent="scrollTo('contact')" class="nav-cta">Hire Me</a>
        <!-- Hamburger -->
        <button class="hamburger" @click="mobileMenuOpen = !mobileMenuOpen" :class="{ active: mobileMenuOpen }">
          <span></span><span></span><span></span>
        </button>
      </div>
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
            <span class="badge-dot"></span>
            Available for work
          </div>

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
            <button class="btn-ghost" @click="downloadCV">
              <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M21 15v4a2 2 0 01-2 2H5a2 2 0 01-2-2v-4"/><polyline points="7 10 12 15 17 10"/><line x1="12" y1="15" x2="12" y2="3"/></svg>
              Download CV
            </button>
          </div>

          <!-- Social links -->
          <div class="hero-socials">
            <a v-for="s in socials" :key="s.name" :href="s.url" target="_blank" rel="noopener" class="social-link" :title="s.name">
              <span v-html="s.svg"></span>
            </a>
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
          v-for="(stat, i) in stats" :key="i"
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
            <p>I'm a passionate frontend developer based in Rwanda, focused on building modern, responsive websites that solve real-world problems.</p>
            <p>My approach combines clean code with beautiful interfaces — every project I build prioritizes both performance and the user experience.</p>
            <p>When I'm not coding, I'm exploring new design trends and pushing the boundaries of what's possible on the web.</p>
            <div class="about-tags">
              <span v-for="t in aboutTags" :key="t" class="about-tag">{{ t }}</span>
            </div>
          </div>
          <div class="about-cards" :class="{ visible: aboutVisible }">
            <div
              v-for="(card, i) in aboutCards" :key="i"
              class="about-card"
              :style="{ transitionDelay: `${i * 80}ms` }"
            >
              <div class="ac-icon" v-html="card.icon"></div>
              <div>
                <h4>{{ card.title }}</h4>
                <p>{{ card.desc }}</p>
              </div>
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

        <div class="skill-logos">
          <div
            v-for="(skill, i) in skills" :key="skill.name"
            class="skill-logo-card"
            :class="{ visible: skillsVisible }"
            :style="{ transitionDelay: `${i * 60}ms` }"
          >
            <div class="slc-icon" v-html="skill.svg"></div>
            <div class="slc-info">
              <span class="slc-name">{{ skill.name }}</span>
              <div class="slc-bar-bg">
                <div
                  class="slc-bar-fill"
                  :style="{
                    width: skillsVisible ? skill.level + '%' : '0%',
                    transitionDelay: `${i * 60 + 300}ms`
                  }"
                ></div>
              </div>
            </div>
            <span class="slc-pct">{{ skill.level }}%</span>
          </div>
        </div>

        <div class="tools-row">
          <span
            v-for="(tool, i) in tools" :key="tool.name"
            class="tool-pill"
            :class="{ visible: skillsVisible }"
            :style="{ transitionDelay: `${i * 50 + 500}ms` }"
          >
            <span class="tp-icon" v-html="tool.svg"></span>
            {{ tool.name }}
          </span>
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
            v-for="(project, i) in projects" :key="project.title"
            class="project-card"
            :class="{ visible: projectsVisible }"
            :style="{ transitionDelay: `${i * 100}ms` }"
            @mouseenter="activeProject = i"
            @mouseleave="activeProject = null"
          >
            <div class="pc-image">
              <img :src="project.img" :alt="project.title" />
              <!-- WIP overlay -->
              <div v-if="project.wip" class="pc-overlay pc-overlay-wip" :class="{ active: activeProject === i }">
                <div class="wip-badge">
                  <svg width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><circle cx="12" cy="12" r="10"/><line x1="12" y1="8" x2="12" y2="12"/><line x1="12" y1="16" x2="12.01" y2="16"/></svg>
                  Not Yet Finished
                </div>
                <p class="wip-sub">Coming soon — work in progress</p>
              </div>
              <!-- Normal overlay -->
              <div v-else class="pc-overlay" :class="{ active: activeProject === i }">
                <a :href="project.url" target="_blank" rel="noopener" class="pc-btn">View Project</a>
                <a v-if="project.github" :href="project.github" target="_blank" rel="noopener" class="pc-btn pc-btn-ghost">GitHub</a>
              </div>
            </div>
            <div class="pc-body">
              <div class="pc-tags">
                <span v-for="tag in project.tags" :key="tag" class="pc-tag">{{ tag }}</span>
                <span v-if="project.wip" class="pc-tag pc-tag-wip">In Progress</span>
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
            <p class="contact-sub">Have a project in mind? I'd love to hear about it. Send me a message and let's make something great.</p>
            <div class="contact-info">
              <div class="ci-item" v-for="item in contactInfo" :key="item.label">
                <div class="ci-icon" v-html="item.icon"></div>
                <div>
                  <span class="ci-label">{{ item.label }}</span>
                  <span class="ci-value">{{ item.value }}</span>
                </div>
              </div>
            </div>
            <!-- Social links in contact -->
            <div class="contact-socials">
              <a v-for="s in socials" :key="s.name" :href="s.url" target="_blank" rel="noopener" class="social-link social-link-lg" :title="s.name">
                <span v-html="s.svg"></span>
              </a>
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
               
                <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M22 2L11 13M22 2l-7 20-4-9-9-4 20-7z"/> Send Message</svg>
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
        <!-- Footer socials -->
        <div class="footer-socials">
          <a v-for="s in socials" :key="s.name" :href="s.url" target="_blank" rel="noopener" class="footer-social" :title="s.name">
            <span v-html="s.svg"></span>
          </a>
        </div>
        <p class="footer-copy">© 2026 Josue. All rights reserved.</p>
      </div>
    </footer>

    <!-- BACK TO TOP -->
    <button class="back-to-top" :class="{ show: isScrolled }" @click="scrollTo('hero')" title="Back to top">
      <svg width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5">
        <path d="M18 15l-6-6-6 6"/>
      </svg>
    </button>

  </div>
</template>

<script>
export default {
  name: 'Portfolio',
  data() {
    return {
      isScrolled:      false,
      isLight:         false,
      mobileMenuOpen:  false,
      heroVisible:     false,
      statsVisible:    false,
      aboutVisible:    false,
      skillsVisible:   false,
      projectsVisible: false,
      contactVisible:  false,
      activeProject:   null,
      formSent:        false,
      form: { name: '', email: '', subject: '', message: '' },

      socials: [
        {
          name: 'GitHub',
          url: 'https://github.com/IGIRANEZA-josue',
          svg: `<svg width="18" height="18" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg" fill="currentColor"><path d="M12 .297c-6.63 0-12 5.373-12 12 0 5.303 3.438 9.8 8.205 11.385.6.113.82-.258.82-.577 0-.285-.01-1.04-.015-2.04-3.338.724-4.042-1.61-4.042-1.61C4.422 18.07 3.633 17.7 3.633 17.7c-1.087-.744.084-.729.084-.729 1.205.084 1.838 1.236 1.838 1.236 1.07 1.835 2.809 1.305 3.495.998.108-.776.417-1.305.76-1.605-2.665-.3-5.466-1.332-5.466-5.93 0-1.31.465-2.38 1.235-3.22-.135-.303-.54-1.523.105-3.176 0 0 1.005-.322 3.3 1.23.96-.267 1.98-.399 3-.405 1.02.006 2.04.138 3 .405 2.28-1.552 3.285-1.23 3.285-1.23.645 1.653.24 2.873.12 3.176.765.84 1.23 1.91 1.23 3.22 0 4.61-2.805 5.625-5.475 5.92.42.36.81 1.096.81 2.22 0 1.606-.015 2.896-.015 3.286 0 .315.21.69.825.57C20.565 22.092 24 17.592 24 12.297c0-6.627-5.373-12-12-12"/></svg>`
        },
        {
          name: 'LinkedIn',
          url: 'https://www.linkedin.com/in/igiraneza-kabundege-mugisha-josue-a06023409/',
          svg: `<svg width="18" height="18" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg" fill="currentColor"><path d="M20.447 20.452h-3.554v-5.569c0-1.328-.027-3.037-1.852-3.037-1.853 0-2.136 1.445-2.136 2.939v5.667H9.351V9h3.414v1.561h.046c.477-.9 1.637-1.85 3.37-1.85 3.601 0 4.267 2.37 4.267 5.455v6.286zM5.337 7.433a2.062 2.062 0 01-2.063-2.065 2.064 2.064 0 112.063 2.065zm1.782 13.019H3.555V9h3.564v11.452zM22.225 0H1.771C.792 0 0 .774 0 1.729v20.542C0 23.227.792 24 1.771 24h20.451C23.2 24 24 23.227 24 22.271V1.729C24 .774 23.2 0 22.222 0h.003z"/></svg>`
        },
        {
          name: 'Instagram',
          url: 'https://www.instagram.com/mki_josue/',
          svg: `<svg width="18" height="18" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg" fill="currentColor"><path d="M12 2.163c3.204 0 3.584.012 4.85.07 3.252.148 4.771 1.691 4.919 4.919.058 1.265.069 1.645.069 4.849 0 3.205-.012 3.584-.069 4.849-.149 3.225-1.664 4.771-4.919 4.919-1.266.058-1.644.07-4.85.07-3.204 0-3.584-.012-4.849-.07-3.26-.149-4.771-1.699-4.919-4.92-.058-1.265-.07-1.644-.07-4.849 0-3.204.013-3.583.07-4.849.149-3.227 1.664-4.771 4.919-4.919 1.266-.057 1.645-.069 4.849-.069zM12 0C8.741 0 8.333.014 7.053.072 2.695.272.273 2.69.073 7.052.014 8.333 0 8.741 0 12c0 3.259.014 3.668.072 4.948.2 4.358 2.618 6.78 6.98 6.98C8.333 23.986 8.741 24 12 24c3.259 0 3.668-.014 4.948-.072 4.354-.2 6.782-2.618 6.979-6.98.059-1.28.073-1.689.073-4.948 0-3.259-.014-3.667-.072-4.947-.196-4.354-2.617-6.78-6.979-6.98C15.668.014 15.259 0 12 0zm0 5.838a6.162 6.162 0 100 12.324 6.162 6.162 0 000-12.324zM12 16a4 4 0 110-8 4 4 0 010 8zm6.406-11.845a1.44 1.44 0 100 2.881 1.44 1.44 0 000-2.881z"/></svg>`
        },
      ],

      stats: [
        { num: '10+',  label: 'Projects Completed' },
        { num: '5+',   label: 'Web Applications'   },
        { num: '2+',   label: 'Years of Learning'  },
        { num: '100%', label: 'Passion for Code'   },
      ],

      aboutTags: ['Problem Solver', 'Detail-Oriented', 'Fast Learner', 'Team Player'],

      aboutCards: [
        {
          icon: `<svg width="22" height="22" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.8"><polyline points="16 18 22 12 16 6"/><polyline points="8 6 2 12 8 18"/></svg>`,
          title: 'Frontend Dev',
          desc:  'Building responsive, accessible UIs with Vue.js and modern CSS.',
        },
        {
          icon: `<svg width="22" height="22" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.8"><circle cx="12" cy="12" r="3"/><path d="M19.07 4.93a10 10 0 010 14.14"/><path d="M4.93 4.93a10 10 0 000 14.14"/></svg>`,
          title: 'UI Designer',
          desc:  'Crafting beautiful, intuitive interfaces users actually enjoy.',
        },
        {
          icon: `<svg width="22" height="22" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.8"><path d="M12 2L2 7l10 5 10-5-10-5zM2 17l10 5 10-5M2 12l10 5 10-5"/></svg>`,
          title: 'Web Apps',
          desc:  'Delivering full-featured apps with clean architecture and great UX.',
        },
      ],

      skills: [
        {
          name: 'HTML5', level: 92,
          svg: `<svg viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg" width="32" height="32"><path d="M1.5 0h21l-1.91 21.563L11.977 24l-8.564-2.438L1.5 0zm7.031 9.75l-.232-2.718 10.059.003.23-2.622L5.412 4.41l.698 8.01h9.126l-.326 3.426-2.91.804-2.955-.81-.188-2.11H6.248l.33 4.171L12 19.351l5.379-1.443.744-8.157H8.531z" fill="#E34F26"/></svg>`
        },
        {
          name: 'CSS3', level: 88,
          svg: `<svg viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg" width="32" height="32"><path d="M1.5 0h21l-1.91 21.563L11.977 24l-8.565-2.438L1.5 0zm17.09 4.413L5.41 4.41l.213 2.622 10.125.002-.255 2.716h-6.64l.24 2.573h6.182l-.366 3.523-2.91.804-2.956-.81-.188-2.11h-2.61l.33 4.171L12 19.351l5.379-1.443.744-8.157H8.374L8.031 9.75l8.633-.002.246-2.622H5.254" fill="#1572B6"/></svg>`
        },
        {
          name: 'JavaScript', level: 85,
          svg: `<svg viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg" width="32" height="32"><path d="M0 0h24v24H0V0zm22.034 18.276c-.175-1.095-.888-2.015-3.003-2.873-.736-.345-1.554-.585-1.797-1.14-.091-.33-.105-.51-.046-.705.15-.646.915-.84 1.515-.66.39.12.75.42.976.9 1.034-.676 1.034-.676 1.755-1.125-.27-.42-.404-.601-.586-.78-.63-.705-1.469-1.065-2.834-1.034l-.705.089c-.676.165-1.32.525-1.71 1.005-1.14 1.291-.811 3.541.569 4.471 1.365 1.02 3.361 1.244 3.616 2.205.24 1.17-.87 1.545-1.966 1.41-.811-.18-1.26-.586-1.755-1.336l-1.83 1.051c.21.48.45.689.81 1.109 1.74 1.756 6.09 1.666 6.871-1.004.029-.09.24-.705.074-1.65l.046.067zm-8.983-7.245h-2.248c0 1.938-.009 3.864-.009 5.805 0 1.232.063 2.363-.138 2.711-.33.689-1.18.601-1.566.48-.396-.196-.597-.466-.83-.855-.063-.105-.11-.196-.127-.196l-1.825 1.125c.305.63.75 1.172 1.324 1.517.855.51 2.004.675 3.207.405.783-.226 1.458-.691 1.811-1.411.51-.93.402-2.07.397-3.346.012-2.054 0-4.109 0-6.179l.004-.056z" fill="#F7DF1E"/></svg>`
        },
        {
          name: 'Vue.js', level: 90,
          svg: `<svg viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg" width="32" height="32"><path d="M24 1.61h-9.94L12 5.16 9.94 1.61H0l12 20.78L24 1.61zM12 14.08L5.16 2.23h4.03L12 6.41l2.81-4.18h4.03L12 14.08z" fill="#42b883"/></svg>`
        },
        {
          name: 'Tailwind CSS', level: 80,
          svg: `<svg viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg" width="32" height="32"><path d="M12.001 4.8c-3.2 0-5.2 1.6-6 4.8 1.2-1.6 2.6-2.2 4.2-1.8.913.228 1.565.89 2.288 1.624C13.666 10.618 15.027 12 18.001 12c3.2 0 5.2-1.6 6-4.8-1.2 1.6-2.6 2.2-4.2 1.8-.913-.228-1.565-.89-2.288-1.624C16.337 6.182 14.976 4.8 12.001 4.8zm-6 7.2c-3.2 0-5.2 1.6-6 4.8 1.2-1.6 2.6-2.2 4.2-1.8.913.228 1.565.89 2.288 1.624 1.177 1.194 2.538 2.576 5.512 2.576 3.2 0 5.2-1.6 6-4.8-1.2 1.6-2.6 2.2-4.2 1.8-.913-.228-1.565-.89-2.288-1.624C10.337 13.382 8.976 12 6.001 12z" fill="#06B6D4"/></svg>`
        },
        {
          name: 'GitHub', level: 78,
          svg: `<svg viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg" width="32" height="32"><path d="M12 .297c-6.63 0-12 5.373-12 12 0 5.303 3.438 9.8 8.205 11.385.6.113.82-.258.82-.577 0-.285-.01-1.04-.015-2.04-3.338.724-4.042-1.61-4.042-1.61C4.422 18.07 3.633 17.7 3.633 17.7c-1.087-.744.084-.729.084-.729 1.205.084 1.838 1.236 1.838 1.236 1.07 1.835 2.809 1.305 3.495.998.108-.776.417-1.305.76-1.605-2.665-.3-5.466-1.332-5.466-5.93 0-1.31.465-2.38 1.235-3.22-.135-.303-.54-1.523.105-3.176 0 0 1.005-.322 3.3 1.23.96-.267 1.98-.399 3-.405 1.02.006 2.04.138 3 .405 2.28-1.552 3.285-1.23 3.285-1.23.645 1.653.24 2.873.12 3.176.765.84 1.23 1.91 1.23 3.22 0 4.61-2.805 5.625-5.475 5.92.42.36.81 1.096.81 2.22 0 1.606-.015 2.896-.015 3.286 0 .315.21.69.825.57C20.565 22.092 24 17.592 24 12.297c0-6.627-5.373-12-12-12" fill="#181717"/></svg>`
        },
      ],

      tools: [
        { name: 'Vue Router',
          svg: `<svg viewBox="0 0 24 24" width="14" height="14" fill="none" stroke="#2563eb" stroke-width="2"><path d="M24 1.61h-9.94L12 5.16 9.94 1.61H0l12 20.78L24 1.61z"/></svg>` },
        { name: 'Pinia',
          svg: `<svg viewBox="0 0 24 24" width="14" height="14" fill="none" stroke="#f59e0b" stroke-width="2"><path d="M12 2C8 2 5 5 5 9c0 5 7 13 7 13s7-8 7-13c0-4-3-7-7-7z"/></svg>` },
        { name: 'Vite',
          svg: `<svg viewBox="0 0 24 24" width="14" height="14" fill="none" stroke="#646cff" stroke-width="2"><path d="M2 3l10 18L22 3"/><path d="M2 3h10v10"/></svg>` },
        { name: 'Figma',
          svg: `<svg viewBox="0 0 24 24" width="14" height="14" xmlns="http://www.w3.org/2000/svg"><path d="M8 24c2.208 0 4-1.792 4-4v-4H8c-2.208 0-4 1.792-4 4s1.792 4 4 4z" fill="#0ACF83"/><path d="M4 12c0-2.208 1.792-4 4-4h4v8H8c-2.208 0-4-1.792-4-4z" fill="#A259FF"/><path d="M4 4c0-2.208 1.792-4 4-4h4v8H8C5.792 8 4 6.208 4 4z" fill="#F24E1E"/><path d="M12 0h4c2.208 0 4 1.792 4 4s-1.792 4-4 4h-4V0z" fill="#FF7262"/><path d="M20 12c0 2.208-1.792 4-4 4s-4-1.792-4-4 1.792-4 4-4 4 1.792 4 4z" fill="#1ABCFE"/></svg>` },
        { name: 'Git',
          svg: `<svg viewBox="0 0 24 24" width="14" height="14" xmlns="http://www.w3.org/2000/svg"><path d="M23.546 10.93L13.067.452c-.604-.603-1.582-.603-2.188 0L8.708 2.627l2.76 2.76c.645-.215 1.379-.07 1.889.441.516.515.658 1.258.438 1.9l2.658 2.66c.645-.223 1.387-.078 1.9.435.721.72.721 1.884 0 2.604-.719.719-1.881.719-2.6 0-.539-.541-.674-1.337-.404-1.996L12.86 8.955v6.525c.176.086.342.203.488.348.713.721.713 1.883 0 2.6-.719.721-1.889.721-2.609 0-.719-.719-.719-1.879 0-2.598.182-.18.387-.316.605-.406V8.835c-.217-.091-.424-.222-.6-.401-.545-.545-.676-1.342-.396-2.009L7.636 3.7.45 10.881c-.6.605-.6 1.584 0 2.189l10.48 10.477c.604.604 1.582.604 2.186 0l10.43-10.43c.605-.603.605-1.582 0-2.187" fill="#F05032"/></svg>` },
        { name: 'REST APIs',
          svg: `<svg viewBox="0 0 24 24" width="14" height="14" fill="none" stroke="#2563eb" stroke-width="2"><path d="M18 8h1a4 4 0 010 8h-1"/><path d="M2 8h16v9a4 4 0 01-4 4H6a4 4 0 01-4-4V8z"/><line x1="6" y1="1" x2="6" y2="4"/><line x1="10" y1="1" x2="10" y2="4"/><line x1="14" y1="1" x2="14" y2="4"/></svg>` },
        { name: 'Netlify',
          svg: `<svg viewBox="0 0 24 24" width="14" height="14" xmlns="http://www.w3.org/2000/svg"><path d="M16.934 8.519a1.044 1.044 0 01.303.23l2.349-1.045-2.652-.652v1.467zm.161 1.238a1.044 1.044 0 01-1.06 1.06 1.069 1.069 0 01-.244-.029l-1.671 2.836c.024.076.04.155.04.238a1.044 1.044 0 01-2.089 0 1.07 1.07 0 01.086-.42l-1.844-1.377a1.04 1.04 0 01-.567.167 1.044 1.044 0 01-1.044-1.044c0-.35.172-.658.436-.847V6.899a1.044 1.044 0 11.943-1.84l1.964-1.151a1.042 1.042 0 011.02-1.254 1.044 1.044 0 011.04.956l2.664.654-.025.028 1.78 2.414a1.044 1.044 0 01-.579 1.051zM0 15.517l1.481 1.48.67-1.48zm2.948 2.946l6.953 2.538-1.498-2.538zm1.915-4.397L6.74 15.04l-2.45 1.452zm.375-.84l4.111-2.437a1.04 1.04 0 00.424.09c.057 0 .11-.009.166-.016l1.237 5.553H9.12zm7.26 3.095l1.303 2.208 3.617-3.617-1.247-.73zm3.81-3.51l2.49 1.46-.003-2.92zm1.302 4.81L24 24v-4.906zM0 16.517V24l6.515-4.882z" fill="#00C7B7"/></svg>` },
        { name: 'Responsive Design',
          svg: `<svg viewBox="0 0 24 24" width="14" height="14" fill="none" stroke="#2563eb" stroke-width="2"><rect x="5" y="2" width="14" height="20" rx="2"/><line x1="12" y1="18" x2="12" y2="18"/></svg>` },
      ],

      projects: [
        {
          title: 'Beta Tech Solution Limited',
          desc:  'A full web system for Beta Tech Solution Limited — a technology company delivering modern digital solutions and services.',
          img:   'https://images.unsplash.com/photo-1498050108023-c5249f4df085?w=800',
          tags:  ['Vue.js', 'Platform', 'UX'],
          url:   'https://github.com/Arnaud090/Beta-tech-web-system',
          github: 'https://github.com/Arnaud090/Beta-tech-web-system',
        },
        {
          title: 'Tembera Rwanda',
          desc:  "Tourism website showcasing Rwanda's stunning attractions, culture and hospitality.",
          img:   'https://images.unsplash.com/photo-1469474968028-56623f02e42e?w=800',
          tags:  ['Vue.js', 'Tourism', 'Design'],
          url:   'https://github.com/IGIRANEZA-josue/TEMBERURWANDA',
          github: 'https://github.com/IGIRANEZA-josue/TEMBERURWANDA',
        },
        {
          title: 'School Portal',
          desc:  'Vue Router application with multiple pages, student dashboards and responsive design.',
          img:   'https://images.unsplash.com/photo-1516321318423-f06f85e504b3?w=800',
          tags:  ['Vue Router', 'Dashboard', 'Education'],
          url:   '#',
          github: null,
          wip:   true,
        },
      ],

      contactInfo: [
        {
          icon: `<svg width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M4 4h16c1.1 0 2 .9 2 2v12c0 1.1-.9 2-2 2H4c-1.1 0-2-.9-2-2V6c0-1.1.9-2 2-2z"/><polyline points="22,6 12,13 2,6"/></svg>`,
          label: 'Email',
          value: 'kabundege.jr@email.com',
        },
        {
          icon: `<svg width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M21 10c0 7-9 13-9 13s-9-6-9-13a9 9 0 0118 0z"/><circle cx="12" cy="10" r="3"/></svg>`,
          label: 'Location',
          value: 'Kigali, Rwanda',
        },
        {
          icon: `<svg width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M22 16.92v3a2 2 0 01-2.18 2 19.79 19.79 0 01-8.63-3.07A19.5 19.5 0 013.07 9.81 19.79 19.79 0 01.1 1.18 2 2 0 012.08.01h3a2 2 0 012 1.72c.127.96.361 1.903.7 2.81a2 2 0 01-.45 2.11L6.09 7.91a16 16 0 006 6l1.27-1.27a2 2 0 012.11-.45c.907.339 1.85.573 2.81.7A2 2 0 0122 16.92z"/></svg>`,
          label: 'Phone / WhatsApp',
          value: '+250 700 000 000',
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
    onScroll() { this.isScrolled = window.scrollY > 60 },

    scrollTo(id) {
      const el = document.getElementById(id)
      if (el) el.scrollIntoView({ behavior: 'smooth' })
    },

    navTo(id) {
      this.mobileMenuOpen = false
      this.scrollTo(id)
    },

    // ── Download CV ──
    // Place your CV PDF at /public/Josue_CV.pdf in your Vue project.
    // The file will then be served at the root URL and this will download it directly.
    // Alternatively replace cvUrl with a direct Google Drive download link:
    // e.g. 'https://drive.google.com/uc?export=download&id=YOUR_FILE_ID'
    downloadCV() {
      const cvUrl = '/Josue_CV.pdf' // ← put Josue_CV.pdf inside your /public folder
      const link = document.createElement('a')
      link.href = cvUrl
      link.setAttribute('download', 'Josue_CV.pdf')
      link.setAttribute('target', '_blank')
      document.body.appendChild(link)
      link.click()
      document.body.removeChild(link)
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
      observe('.stats-bar',        'statsVisible',    0.3)
      observe('.about-section',    'aboutVisible',    0.2)
      observe('.skills-section',   'skillsVisible',   0.2)
      observe('.projects-section', 'projectsVisible', 0.1)
      observe('.contact-section',  'contactVisible',  0.15)
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
/* ── TOKENS: dark (default) ── */
.portfolio {
  --bg:        #05091a;
  --bg2:       #080d22;
  --bg3:       #0c1229;
  --surface:   #0f1635;
  --surf2:     #131c40;
  --border:    rgba(37,99,235,0.15);
  --border2:   rgba(37,99,235,0.25);
  --text:      #e8edf8;
  --muted:     #7a8ab8;
  --accent:    #2563eb;
  --accent2:   #60a5fa;
  --accent3:   #93c5fd;
  --green:     #34d399;
  --grad:      linear-gradient(135deg, #1d4ed8, #2563eb, #3b82f6, #60a5fa);
  --radius:    16px;
  --radius-sm: 10px;
  --nav-h:     72px;
  --shadow:    0 8px 32px rgba(37,99,235,0.18);
}

/* ── TOKENS: light ── */
.portfolio.light {
  --bg:      #f0f5ff;
  --bg2:     #e8f0fe;
  --bg3:     #dbeafe;
  --surface: #ffffff;
  --surf2:   #f8faff;
  --border:  rgba(37,99,235,0.12);
  --border2: rgba(37,99,235,0.22);
  --text:    #0f172a;
  --muted:   #475569;
  --shadow:  0 8px 32px rgba(37,99,235,0.10);
}

/* ── RESET ── */
* { margin: 0; padding: 0; box-sizing: border-box; }
.portfolio {
  background: var(--bg);
  color: var(--text);
  font-family: 'Segoe UI', system-ui, sans-serif;
  overflow-x: hidden;
  transition: background 0.4s, color 0.4s;
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
  background: rgba(5,9,26,0.88);
  backdrop-filter: blur(16px);
  border-bottom: 1px solid var(--border);
}
.light.scrolled .nav {
  background: rgba(240,245,255,0.88);
}
.nav-logo {
  font-size: 1.9rem;
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
  letter-spacing: 0.4px;
  transition: color 0.2s;
}
.nav-links a:hover { color: var(--text); }
.nav-right {
  display: flex;
  align-items: center;
  gap: 14px;
  margin-left: 36px;
}

/* Theme toggle */
.theme-toggle {
  width: 40px; height: 40px;
  background: var(--surface);
  border: 1px solid var(--border2);
  border-radius: 50%;
  display: flex; align-items: center; justify-content: center;
  cursor: pointer; color: var(--muted);
  transition: background 0.2s, border-color 0.2s, color 0.2s, transform 0.2s;
}
.theme-toggle:hover { background: var(--bg3); color: var(--accent); transform: rotate(20deg); }

.nav-cta {
  background: var(--accent); color: #fff;
  padding: 10px 24px; border-radius: 50px;
  font-size: 0.9rem; font-weight: 600;
  transition: opacity 0.2s, transform 0.2s;
}
.nav-cta:hover { opacity: 0.85; transform: translateY(-1px); }

/* Hamburger */
.hamburger {
  display: none; flex-direction: column; justify-content: space-between;
  width: 28px; height: 20px; background: none; border: none; cursor: pointer; padding: 0;
}
.hamburger span {
  display: block; height: 2px; background: var(--text); border-radius: 2px;
  transition: transform 0.3s, opacity 0.3s;
  transform-origin: center;
}
.hamburger.active span:nth-child(1) { transform: translateY(9px) rotate(45deg); }
.hamburger.active span:nth-child(2) { opacity: 0; }
.hamburger.active span:nth-child(3) { transform: translateY(-9px) rotate(-45deg); }

/* ── HERO ── */
.hero {
  position: relative;
  min-height: 100vh;
  display: flex; flex-direction: column; align-items: center; justify-content: center;
  padding: var(--nav-h) 7% 80px;
  overflow: hidden;
}
.hero-bg { position: absolute; inset: 0; pointer-events: none; }
.grid-overlay {
  position: absolute; inset: 0;
  background-image:
    linear-gradient(rgba(37,99,235,0.06) 1px, transparent 1px),
    linear-gradient(90deg, rgba(37,99,235,0.06) 1px, transparent 1px);
  background-size: 60px 60px;
}
.glow { position: absolute; border-radius: 50%; filter: blur(120px); opacity: 0.22; }
.glow-1 { width: 600px; height: 600px; top: -100px; left: -100px; background: #2563eb; }
.glow-2 { width: 400px; height: 400px; bottom: -80px; right: 5%; background: #60a5fa; opacity: 0.14; }

.hero-inner {
  display: flex; align-items: center; justify-content: space-between;
  gap: 80px; width: 100%; max-width: 1200px; z-index: 1;
}
.hero-text {
  flex: 1;
  opacity: 0; transform: translateY(30px);
  transition: opacity 0.8s, transform 0.8s;
}
.hero-text.visible { opacity: 1; transform: translateY(0); }

.badge {
  display: inline-flex; align-items: center; gap: 8px;
  background: rgba(52,211,153,0.1); border: 1px solid rgba(52,211,153,0.3);
  color: var(--green);
  padding: 8px 18px; border-radius: 50px;
  font-size: 0.82rem; font-weight: 600; letter-spacing: 0.5px; margin-bottom: 28px;
}
.badge-dot {
  width: 8px; height: 8px; background: var(--green); border-radius: 50%;
  animation: pulse 2s infinite;
}
@keyframes pulse { 0%, 100% { opacity: 1; } 50% { opacity: 0.3; } }

.hero-title {
  font-size: clamp(3rem, 6vw, 5.5rem);
  font-weight: 800; line-height: 1.05; letter-spacing: -2px; margin-bottom: 20px;
}
.name-gradient {
  background: var(--grad);
  -webkit-background-clip: text; -webkit-text-fill-color: transparent; background-clip: text;
}
.hero-role { font-size: 1.1rem; color: var(--muted); font-weight: 500; margin-bottom: 20px; letter-spacing: 0.5px; }
.sep { margin: 0 10px; color: var(--accent); }
.hero-desc { font-size: 1rem; color: var(--muted); line-height: 1.8; max-width: 480px; margin-bottom: 40px; }
.hero-actions { display: flex; gap: 16px; flex-wrap: wrap; margin-bottom: 36px; }

/* Buttons */
.btn-primary {
  display: inline-flex; align-items: center; gap: 10px;
  background: var(--accent); color: #fff;
  border: none; padding: 15px 32px; border-radius: 50px;
  font-size: 0.95rem; font-weight: 600; font-family: inherit; cursor: pointer;
  transition: transform 0.25s, opacity 0.25s, box-shadow 0.25s;
  box-shadow: 0 4px 20px rgba(37,99,235,0.35);
}
.btn-primary:hover { transform: translateY(-3px); box-shadow: 0 8px 28px rgba(37,99,235,0.45); }
.btn-ghost {
  display: inline-flex; align-items: center; gap: 10px;
  background: transparent; color: var(--text);
  border: 1.5px solid var(--border2);
  padding: 15px 32px; border-radius: 50px;
  font-size: 0.95rem; font-weight: 600; font-family: inherit; cursor: pointer;
  transition: border-color 0.2s, background 0.2s;
}
.btn-ghost:hover { border-color: var(--accent); background: rgba(37,99,235,0.08); }

/* ── SOCIAL LINKS ── */
.hero-socials {
  display: flex; gap: 12px; align-items: center;
}
.social-link {
  width: 42px; height: 42px;
  background: var(--surface);
  border: 1px solid var(--border2);
  border-radius: 50%;
  display: flex; align-items: center; justify-content: center;
  color: var(--muted);
  transition: color 0.25s, border-color 0.25s, background 0.25s, transform 0.25s;
}
.social-link:hover {
  color: var(--accent2);
  border-color: var(--accent);
  background: rgba(37,99,235,0.1);
  transform: translateY(-3px);
}
/* Larger variant for contact section */
.social-link-lg {
  width: 48px; height: 48px;
}
.contact-socials {
  display: flex; gap: 12px; margin-top: 32px;
}

/* Hero image */
.hero-image {
  position: relative; flex-shrink: 0;
  opacity: 0; transform: translateX(30px);
  transition: opacity 0.9s 0.2s, transform 0.9s 0.2s;
}
.hero-image.visible { opacity: 1; transform: translateX(0); }
.img-frame { position: relative; width: 360px; height: 450px; }
.img-frame img {
  width: 100%; height: 100%; object-fit: cover; border-radius: 24px;
  display: block; position: relative; z-index: 1;
}
.img-border {
  position: absolute; inset: -3px; border-radius: 26px;
  background: var(--grad); z-index: 0; opacity: 0.7;
}
.float-card {
  position: absolute;
  background: var(--surface); border: 1px solid var(--border2); border-radius: var(--radius-sm);
  padding: 14px 20px; display: flex; flex-direction: column; align-items: center;
  backdrop-filter: blur(10px); z-index: 2; box-shadow: var(--shadow);
}
.card-exp  { bottom: 30px; left: -60px; }
.card-proj { top: 40px; right: -55px; }
.fc-num {
  font-size: 1.6rem; font-weight: 800; line-height: 1;
  background: var(--grad);
  -webkit-background-clip: text; -webkit-text-fill-color: transparent; background-clip: text;
}
.fc-label { font-size: 0.72rem; color: var(--muted); font-weight: 600; margin-top: 2px; }

/* Scroll hint */
.scroll-hint {
  position: absolute; bottom: 32px; left: 50%; transform: translateX(-50%);
  display: flex; flex-direction: column; align-items: center; gap: 8px;
  cursor: pointer; opacity: 0.45; transition: opacity 0.2s; z-index: 1;
}
.scroll-hint:hover { opacity: 1; }
.scroll-hint span { font-size: 0.72rem; letter-spacing: 2px; color: var(--muted); }
.scroll-mouse {
  width: 24px; height: 38px; border: 2px solid var(--muted); border-radius: 12px;
  display: flex; justify-content: center; padding-top: 6px;
}
.scroll-wheel {
  width: 4px; height: 8px; background: var(--accent); border-radius: 2px;
  animation: scroll-anim 2s infinite;
}
@keyframes scroll-anim { 0% { transform: translateY(0); opacity: 1; } 100% { transform: translateY(10px); opacity: 0; } }

/* ── STATS ── */
.stats-bar {
  background: var(--bg2);
  border-top: 1px solid var(--border); border-bottom: 1px solid var(--border);
  padding: 48px 7%;
}
.stats-inner {
  max-width: 1200px; margin: auto;
  display: flex; justify-content: space-around; flex-wrap: wrap; gap: 30px;
}
.stat-item {
  text-align: center; opacity: 0; transform: translateY(20px);
  transition: opacity 0.6s, transform 0.6s;
}
.stat-item.visible { opacity: 1; transform: translateY(0); }
.stat-num {
  display: block; font-size: 3rem; font-weight: 800; letter-spacing: -1px;
  background: var(--grad);
  -webkit-background-clip: text; -webkit-text-fill-color: transparent; background-clip: text;
  line-height: 1;
}
.stat-label { display: block; font-size: 0.85rem; color: var(--muted); font-weight: 500; margin-top: 6px; }

/* ── SECTIONS ── */
.section { padding: 110px 7%; }
.section-inner { max-width: 1200px; margin: auto; }
.section-label { font-size: 0.72rem; font-weight: 700; letter-spacing: 3px; color: var(--accent); margin-bottom: 16px; }
.section-title { font-size: clamp(2rem, 4vw, 3rem); font-weight: 800; letter-spacing: -1px; margin-bottom: 56px; line-height: 1.1; }

/* ── ABOUT ── */
.about-section { background: var(--bg); }
.about-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 70px; align-items: start; }
.about-text { opacity: 0; transform: translateX(-30px); transition: opacity 0.8s, transform 0.8s; }
.about-text.visible { opacity: 1; transform: translateX(0); }
.about-text p { color: var(--muted); line-height: 1.9; font-size: 1rem; margin-bottom: 20px; }
.about-tags { display: flex; flex-wrap: wrap; gap: 10px; margin-top: 28px; }
.about-tag {
  background: rgba(37,99,235,0.1); border: 1px solid rgba(37,99,235,0.22);
  color: var(--accent2); padding: 8px 18px; border-radius: 50px;
  font-size: 0.82rem; font-weight: 600;
}
.about-cards {
  display: flex; flex-direction: column; gap: 20px;
  opacity: 0; transform: translateX(30px);
  transition: opacity 0.8s 0.2s, transform 0.8s 0.2s;
}
.about-cards.visible { opacity: 1; transform: translateX(0); }
.about-card {
  background: var(--surface); border: 1px solid var(--border); border-radius: var(--radius);
  padding: 26px; display: flex; gap: 18px; align-items: flex-start;
  transition: border-color 0.3s, transform 0.3s, box-shadow 0.3s;
}
.about-card:hover { border-color: var(--accent); transform: translateX(6px); box-shadow: var(--shadow); }
.ac-icon {
  width: 44px; height: 44px; background: rgba(37,99,235,0.1); border-radius: 10px;
  display: flex; align-items: center; justify-content: center; color: var(--accent2); flex-shrink: 0;
}
.about-card h4 { font-size: 1rem; font-weight: 700; margin-bottom: 6px; }
.about-card p { font-size: 0.88rem; color: var(--muted); line-height: 1.6; }

/* ── SKILLS ── */
.skills-section { background: var(--bg2); }
.skill-logos { display: flex; flex-direction: column; gap: 18px; margin-bottom: 48px; }
.skill-logo-card {
  display: flex; align-items: center; gap: 18px;
  background: var(--surface); border: 1px solid var(--border); border-radius: var(--radius-sm);
  padding: 16px 22px;
  opacity: 0; transform: translateX(-20px);
  transition: opacity 0.6s, transform 0.6s, border-color 0.3s, box-shadow 0.3s;
}
.skill-logo-card.visible { opacity: 1; transform: translateX(0); }
.skill-logo-card:hover { border-color: var(--accent); box-shadow: var(--shadow); }
.slc-icon {
  width: 40px; height: 40px; flex-shrink: 0;
  display: flex; align-items: center; justify-content: center;
  background: var(--bg3); border-radius: 8px; padding: 4px;
}
.slc-icon svg { width: 32px; height: 32px; }
.slc-info { flex: 1; }
.slc-name { display: block; font-size: 0.9rem; font-weight: 700; margin-bottom: 8px; }
.slc-bar-bg { height: 6px; background: var(--bg3); border-radius: 3px; overflow: hidden; }
.slc-bar-fill {
  height: 100%; background: var(--grad); border-radius: 3px;
  width: 0; transition: width 1s cubic-bezier(0.4,0,0.2,1);
}
.slc-pct { font-size: 0.8rem; color: var(--accent2); font-weight: 700; min-width: 36px; text-align: right; }
.tools-row { display: flex; flex-wrap: wrap; gap: 10px; }
.tool-pill {
  background: var(--bg3); border: 1px solid var(--border2);
  padding: 9px 16px; border-radius: 50px;
  font-size: 0.82rem; font-weight: 600; color: var(--muted);
  display: flex; align-items: center; gap: 6px;
  opacity: 0; transform: translateY(10px);
  transition: opacity 0.5s, transform 0.5s, color 0.2s, border-color 0.2s, background 0.2s;
}
.tool-pill.visible { opacity: 1; transform: translateY(0); }
.tool-pill:hover { color: var(--text); border-color: var(--accent); background: rgba(37,99,235,0.08); }
.tp-icon { display: flex; align-items: center; }

/* ── PROJECTS ── */
.projects-section { background: var(--bg); }
.projects-grid { display: grid; grid-template-columns: repeat(auto-fill, minmax(320px, 1fr)); gap: 28px; }
.project-card {
  background: var(--surface); border: 1px solid var(--border); border-radius: var(--radius); overflow: hidden;
  opacity: 0; transform: translateY(30px);
  transition: opacity 0.6s, transform 0.6s, border-color 0.3s, box-shadow 0.3s;
}
.project-card.visible { opacity: 1; transform: translateY(0); }
.project-card:hover { border-color: var(--accent); box-shadow: var(--shadow); }
.pc-image { position: relative; height: 220px; overflow: hidden; }
.pc-image img { width: 100%; height: 100%; object-fit: cover; transition: transform 0.5s; display: block; }
.project-card:hover .pc-image img { transform: scale(1.06); }
.pc-overlay {
  position: absolute; inset: 0; background: rgba(5,9,26,0.78);
  display: flex; align-items: center; justify-content: center; gap: 12px;
  opacity: 0; transition: opacity 0.3s;
}
.pc-overlay-wip {
  flex-direction: column; gap: 10px;
  background: rgba(5,9,26,0.88);
}
.wip-badge {
  display: flex; align-items: center; gap: 10px;
  background: rgba(251,191,36,0.15);
  border: 1.5px solid rgba(251,191,36,0.5);
  color: #fbbf24;
  padding: 12px 24px; border-radius: 50px;
  font-size: 1rem; font-weight: 700;
  transform: translateY(10px); transition: transform 0.3s;
}
.pc-overlay-wip.active .wip-badge { transform: translateY(0); }
.wip-sub {
  font-size: 0.8rem; color: rgba(255,255,255,0.5); letter-spacing: 0.5px;
  transform: translateY(10px); transition: transform 0.3s 0.05s; opacity: 0;
}
.pc-overlay-wip.active .wip-sub { transform: translateY(0); opacity: 1; }
.pc-overlay.active { opacity: 1; }
.pc-btn {
  background: var(--accent); color: #fff; border: none;
  padding: 12px 22px; border-radius: 50px;
  font-size: 0.87rem; font-weight: 600; font-family: inherit; cursor: pointer;
  transform: translateY(10px); transition: transform 0.3s, background 0.2s;
  display: inline-flex; align-items: center;
}
.pc-btn-ghost {
  background: transparent; border: 1.5px solid rgba(255,255,255,0.5); color: #fff;
}
.pc-btn-ghost:hover { background: rgba(255,255,255,0.1); border-color: #fff; }
.pc-overlay.active .pc-btn { transform: translateY(0); }
.pc-body { padding: 24px; }
.pc-tags { display: flex; gap: 8px; flex-wrap: wrap; margin-bottom: 14px; }
.pc-tag {
  background: rgba(37,99,235,0.1); color: var(--accent2);
  padding: 4px 12px; border-radius: 50px; font-size: 0.72rem; font-weight: 700; letter-spacing: 0.5px;
}
.pc-tag-wip {
  background: rgba(251,191,36,0.12); color: #fbbf24;
  border: 1px solid rgba(251,191,36,0.3);
}
.pc-body h3 { font-size: 1.2rem; font-weight: 700; margin-bottom: 8px; }
.pc-body p { font-size: 0.88rem; color: var(--muted); line-height: 1.7; }

/* ── CONTACT ── */
.contact-section { background: var(--bg2); }
.contact-inner { display: grid; grid-template-columns: 1fr 1.4fr; gap: 80px; align-items: start; }
.contact-left { opacity: 0; transform: translateX(-30px); transition: opacity 0.8s, transform 0.8s; }
.contact-left.visible { opacity: 1; transform: translateX(0); }
.contact-sub { color: var(--muted); line-height: 1.8; margin-bottom: 40px; margin-top: -30px; }
.contact-info { display: flex; flex-direction: column; gap: 20px; }
.ci-item { display: flex; align-items: center; gap: 16px; }
.ci-icon {
  width: 40px; height: 40px; background: rgba(37,99,235,0.1); border-radius: 10px;
  display: flex; align-items: center; justify-content: center; color: var(--accent2); flex-shrink: 0;
}
.ci-label { display: block; font-size: 0.72rem; color: var(--muted); font-weight: 600; letter-spacing: 0.5px; margin-bottom: 2px; }
.ci-value { display: block; font-size: 0.95rem; font-weight: 600; }

.contact-form {
  background: var(--surface); border: 1px solid var(--border); border-radius: var(--radius); padding: 40px;
  opacity: 0; transform: translateX(30px);
  transition: opacity 0.8s 0.2s, transform 0.8s 0.2s;
}
.contact-form.visible { opacity: 1; transform: translateX(0); }
.form-row { display: grid; grid-template-columns: 1fr 1fr; gap: 16px; }
.form-group { margin-bottom: 20px; }
.form-group label { display: block; font-size: 0.8rem; font-weight: 700; letter-spacing: 0.5px; color: var(--muted); margin-bottom: 8px; }
.form-group input,
.form-group textarea {
  width: 100%; background: var(--bg); border: 1px solid var(--border2); border-radius: var(--radius-sm);
  padding: 13px 16px; color: var(--text); font-family: inherit; font-size: 0.92rem;
  transition: border-color 0.2s; outline: none; resize: vertical;
}
.form-group input:focus,
.form-group textarea:focus { border-color: var(--accent); box-shadow: 0 0 0 3px rgba(37,99,235,0.12); }
.form-group input::placeholder,
.form-group textarea::placeholder { color: rgba(122,138,184,0.5); }
.form-submit { width: 100%; justify-content: center; border-radius: var(--radius-sm); }
.form-submit.sent { background: var(--green); }

/* ── FOOTER ── */
.footer { background: var(--bg); border-top: 1px solid var(--border); padding: 48px 7%; }
.footer-inner {
  max-width: 1200px; margin: auto;
  display: flex; flex-direction: column; align-items: center; gap: 16px; text-align: center;
}
.footer-inner p { font-size: 0.88rem; color: var(--muted); }
.footer-copy { font-size: 0.78rem !important; opacity: 0.5; }
.footer-socials { display: flex; gap: 12px; }
.footer-social {
  width: 38px; height: 38px;
  background: var(--surface); border: 1px solid var(--border2); border-radius: 50%;
  display: flex; align-items: center; justify-content: center;
  color: var(--muted);
  transition: color 0.2s, border-color 0.2s, background 0.2s, transform 0.2s;
}
.footer-social:hover {
  color: var(--accent2); border-color: var(--accent);
  background: rgba(37,99,235,0.1); transform: translateY(-2px);
}

/* ── BACK TO TOP ── */
.back-to-top {
  position: fixed; bottom: 30px; right: 30px; z-index: 99;
  width: 48px; height: 48px;
  background: var(--accent); color: #fff; border: none; border-radius: 50%;
  display: flex; align-items: center; justify-content: center;
  cursor: pointer; box-shadow: 0 4px 20px rgba(37,99,235,0.4);
  opacity: 0; transform: translateY(20px) scale(0.8);
  transition: opacity 0.3s, transform 0.3s, box-shadow 0.2s;
  pointer-events: none;
}
.back-to-top.show { opacity: 1; transform: translateY(0) scale(1); pointer-events: auto; }
.back-to-top:hover { box-shadow: 0 8px 28px rgba(37,99,235,0.5); transform: translateY(-3px) scale(1); }

/* ── RESPONSIVE ── */
@media (max-width: 960px) {
  .hero-inner { flex-direction: column-reverse; text-align: center; gap: 50px; }
  .hero-text  { align-items: center; display: flex; flex-direction: column; }
  .hero-desc  { max-width: 100%; }
  .hero-socials { justify-content: center; }
  .img-frame  { width: 280px; height: 340px; }
  .card-exp   { left: -30px; }
  .card-proj  { right: -30px; }
  .about-grid { grid-template-columns: 1fr; gap: 40px; }
  .contact-inner { grid-template-columns: 1fr; gap: 40px; }
}
@media (max-width: 640px) {
  .nav-links   { 
    display: none; position: fixed; top: var(--nav-h); left: 0; right: 0;
    flex-direction: column; gap: 0; background: var(--bg2);
    border-bottom: 1px solid var(--border); padding: 12px 0;
  }
  .nav-links.open { display: flex; }
  .nav-links li a { display: block; padding: 14px 7%; font-size: 1rem; }
  .nav-cta     { display: none; }
  .hamburger   { display: flex; }
  .section     { padding: 80px 5%; }
  .hero        { padding-left: 5%; padding-right: 5%; }
  .stats-bar   { padding: 40px 5%; }
  .form-row    { grid-template-columns: 1fr; }
  .contact-form { padding: 24px; }
  .float-card  { display: none; }
  .img-frame   { width: 240px; height: 290px; }
  .back-to-top { bottom: 20px; right: 20px; width: 42px; height: 42px; }
}
</style>
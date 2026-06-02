```vue
<template>
  <div class="portfolio">

    <!-- HERO -->
    <section class="hero">
      <div class="hero-container">

        <div class="hero-image">
          <img src="../assets/josue.png" alt="Josue">
        </div>

        <div class="hero-content">

          <span class="tag">Frontend Developer</span>

          <h1>
            Hi, I'm <span class="blue">Josue</span>
          </h1>

          <h3>Vue.js Developer & UI Designer</h3>

          <p>
            Passionate about creating modern websites, responsive
            applications and beautiful user experiences using
            Vue.js, JavaScript, HTML and CSS.
          </p>

          <div class="buttons">
            <button>View Projects</button>
            <button class="outline">Contact Me</button>
          </div>

        </div>

      </div>
    </section>

    <!-- STATS -->

    <section class="stats">

      <div class="stat-card">
        <h2>10+</h2>
        <p>Projects</p>
      </div>

      <div class="stat-card">
        <h2>5+</h2>
        <p>Web Apps</p>
      </div>

      <div class="stat-card">
        <h2>2+</h2>
        <p>Years Learning</p>
      </div>

    </section>

    <!-- ABOUT -->

    <section class="section">

      <h2>About Me</h2>

      <div class="about-card">

        <p>
          I enjoy building modern and responsive websites that
          solve real-world problems. My focus is on creating
          beautiful interfaces and delivering great user
          experiences.
        </p>

      </div>

    </section>

    <!-- SKILLS -->

    <section class="section blue-bg">

      <h2>Skills</h2>

      <div class="skills">

        <div class="skill">HTML5</div>
        <div class="skill">CSS3</div>
        <div class="skill">JavaScript</div>
        <div class="skill">Vue.js</div>
        <div class="skill">Tailwind CSS</div>
        <div class="skill">GitHub</div>

      </div>

    </section>

    <!-- PROJECTS -->

    <section class="section">

      <h2>Featured Projects</h2>

      <div class="projects">

        <div class="project-card">

          <img
            src="https://images.unsplash.com/photo-1498050108023-c5249f4df085?w=800"
          >

          <div class="project-content">
            <h3>AkaziHub</h3>

            <p>
              Platform connecting job seekers, service providers
              and customers.
            </p>

            <button>View Project</button>
          </div>

        </div>

        <div class="project-card">

          <img
            src="data:image/jpeg;base64,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"
          >

          <div class="project-content">
            <h3>Rwanda Tourism</h3>

            <p>
              Tourism website showcasing attractions and culture.
            </p>

            <button>View Project</button>
          </div>

        </div>

        <div class="project-card">

          <img
            src="https://images.unsplash.com/photo-1516321318423-f06f85e504b3?w=800"
          >

          <div class="project-content">
            <h3>school</h3>

            <p>
              Vue Router application with multiple pages and
              responsive design.
            </p>

            <button>View Project</button>
          </div>

        </div>

      </div>

    </section>

    <!-- CONTACT -->

    <section class="section blue-bg">

      <h2>Contact Me</h2>

      <form class="contact-form">

        <input
          type="text"
          placeholder="Your Name"
        >

        <input
          type="email"
          placeholder="Your Email"
        >

        <textarea
          rows="5"
          placeholder="Your Message"
        ></textarea>

        <button>
          Send Message
        </button>

      </form>

    </section>

    <!-- FOOTER -->

    <footer>

      <h3>Josue Portfolio</h3>

      <p>
        Frontend Developer • Vue.js Developer • UI Designer
      </p>

      <p class="copyright">
        © 2026 All Rights Reserved
      </p>

    </footer>

  </div>
</template>

<style>
*{
  margin:0;
  padding:0;
  box-sizing:border-box;
  font-family:'Segoe UI',sans-serif;
}

body{
  background:#fff;
}

.hero{
  min-height:100vh;
  display:flex;
  align-items:center;
  justify-content:center;
  padding:80px 10%;
  background:#f8fbff;
}

.hero-container{
  display:flex;
  align-items:center;
  gap:80px;
  max-width:1200px;
}

.hero-image img{
  width:400px;
  height:500px;
  object-fit:cover;
  border-radius:25px;
  box-shadow:0 20px 40px rgba(37,99,235,.25);
}

.hero-content{
  flex:1;
}

.tag{
  background:#dbeafe;
  color:#2563eb;
  padding:10px 20px;
  border-radius:50px;
  font-weight:bold;
}

.hero-content h1{
  font-size:4rem;
  margin-top:20px;
}

.blue{
  color:#2563eb;
}

.hero-content h3{
  margin:15px 0;
  color:#2563eb;
}

.hero-content p{
  line-height:1.8;
  color:#555;
}

.buttons{
  margin-top:30px;
}

button{
  background:#2563eb;
  color:white;
  border:none;
  padding:15px 30px;
  border-radius:10px;
  cursor:pointer;
  transition:.3s;
}

button:hover{
  transform:translateY(-5px);
}

.outline{
  background:white;
  color:#2563eb;
  border:2px solid #2563eb;
  margin-left:10px;
}

.stats{
  display:flex;
  justify-content:center;
  flex-wrap:wrap;
  gap:25px;
  padding:80px 10%;
}

.stat-card{
  width:250px;
  background:white;
  padding:35px;
  border-radius:20px;
  text-align:center;
  box-shadow:0 10px 25px rgba(0,0,0,.08);
}

.stat-card h2{
  color:#2563eb;
  font-size:3rem;
}

.section{
  padding:100px 10%;
  text-align:center;
}

.section h2{
  margin-bottom:40px;
  font-size:2.5rem;
}

.blue-bg{
  background:#f8fbff;
}

.about-card{
  max-width:800px;
  margin:auto;
  background:white;
  padding:40px;
  border-radius:20px;
  box-shadow:0 10px 25px rgba(0,0,0,.08);
}

.skills{
  display:flex;
  flex-wrap:wrap;
  justify-content:center;
  gap:20px;
}

.skill{
  background:#2563eb;
  color:white;
  padding:15px 30px;
  border-radius:50px;
}

.projects{
  display:flex;
  flex-wrap:wrap;
  justify-content:center;
  gap:30px;
}

.project-card{
  width:350px;
  background:white;
  border-radius:20px;
  overflow:hidden;
  box-shadow:0 10px 25px rgba(0,0,0,.08);
  transition:.3s;
}

.project-card:hover{
  transform:translateY(-10px);
}

.project-card img{
  width:100%;
  height:220px;
  object-fit:cover;
}

.project-content{
  padding:25px;
}

.contact-form{
  max-width:650px;
  margin:auto;
  background:white;
  padding:40px;
  border-radius:20px;
  box-shadow:0 10px 25px rgba(0,0,0,.08);
}

.contact-form input,
.contact-form textarea{
  width:100%;
  padding:15px;
  margin-bottom:15px;
  border:1px solid #ddd;
  border-radius:10px;
}

footer{
  background:#2563eb;
  color:white;
  text-align:center;
  padding:50px;
}

.copyright{
  margin-top:15px;
}

@media(max-width:900px){

  .hero-container{
    flex-direction:column;
    text-align:center;
  }

  .hero-image img{
    width:300px;
    height:400px;
  }

  .hero-content h1{
    font-size:3rem;
  }
}
</style>


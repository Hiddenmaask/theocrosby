<template>
  <!--
  <div class="hero-lightpass-parent">
    <canvas id="hero-lightpass"/>
  </div>
  -->
  <HeaderBar></HeaderBar>
  <HeroPage></HeroPage>
  <InfoCard v-if="show = 1" msg="Welcome to Your Vue.js App"/>
</template>

<script>
import InfoCard from './components/InfoCard.vue'
import HeaderBar from './components/HeaderBar.vue'
import HeroPage from './components/HeroPage.vue'




export default {
  name: 'App',
  components: {
    InfoCard,
    HeaderBar,
    HeroPage,
  },
  data(){
    return{
      show: 0,
      compNum: 3,
    }
  },
  methods:{
    nextShow(){
      this.show += 1;
      if (this.show > this.compNum){
        this.show = this.compNum;
      }
    },
    backShow(){
      this.show -= 1;
      if (this.show < 1) {
        this.show = 1;
      }
    }
  },
  mounted() {
    const html = document.documentElement;
    const canvas = document.getElementById("hero-lightpass");

    if(canvas){
      document.getElementsByTagName("body").style = "#000";
    }
    const context = canvas.getContext("2d");
    const frameCount = 88;
    const currentFrame = index => (
        `dist/assets/plane/ezgif-frame-${index.toString().padStart(3, '0')}.jpg`
    )

    const preloadImages = () => {
      for (let i = 1; i < frameCount; i++) {
        const img = new Image();
        img.src = currentFrame(i);
      }
    };

    const img = new Image()
    img.src = currentFrame(1);
    canvas.width=2000;
    canvas.height=2000;
    img.onload=function(){
      context.drawImage(img, 0, 0);
    }

    const updateImage = index => {
      img.src = currentFrame(index);
      context.drawImage(img, 0, 0);
    }

    window.addEventListener('scroll', () => {
      const scrollTop = html.scrollTop;
      const maxScrollTop = html.scrollHeight - window.innerHeight;
      const scrollFraction = scrollTop / maxScrollTop;
      const frameIndex = Math.min(
          frameCount - 1,
          Math.ceil(scrollFraction * frameCount)
      );

      requestAnimationFrame(() => updateImage(frameIndex + 1))
    });

    preloadImages()
  }
}
</script>


<style>

@import url('https://fonts.googleapis.com/css2?family=League+Spartan:wght@100;200;300;400;500;600;700;800;900&display=swap');

*, *::after, *::before {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

button {
  font: inherit;
  border:none;
  cursor: pointer;
}

input,
label {
  font: inherit;
}


:root{
  --_hue: 191;
  --_size: 2vmax;
  --_radius: .2em;
  --_tspeed_fast: 150ms;
  --_tspeed_slow: 400ms;
  --_ttype_squish: cubic-bezier(0.86,-0.1, 0.27, 1.15);

  /* Light Theme */

  --bg--light: var(--_hue) 49% 95%;
  --txt--light: 0% 3% 20%;
  --accent--light: var(--_hue) 50% 57%;
  --accentalt--light: var(--_hue) 84% 17%;
  --muted--light: var(--_hue) 50% 98%;

  /* Dark Theme */

  --bg--dark: var(--_hue) 49% 95%;
  --txt--dark: 0% 3% 20%;
  --accent--dark: var(--_hue) 50% 57%;
  --accentalt--dark: var(--_hue) 84% 17%;
  --muted--dark: var(--_hue) 50% 98;

  /* Defaults */

  --bg: var(--bg--light);
  --txt: var(--txt--light);
  --accent: var(--accent--light);
  --accentalt: var(--accentalt--light);
  --muted: var(--muted--light);
  color-scheme: light;


}

/* @Media controls */

@media (prefers-color-scheme: dark){
  :root{
    --bg: var(--bg--dark);
    --txt: var(--txt--dark);
    --accent: var(--accent--dark);
    --accentalt: var(--accentalt--dark);
    --muted: var(--muted--dark);
    color-scheme: dark;
  }
}

/* Prefers reduced motion */

@media (prefers-reduced-motion: reduce) {
  :root{
    --_tspeed_fast: 50ms;
    --_tspeed_slow: 100ms;

  }
}

#app{
  height: 100%;
  width: 100%;

}
body{
  background-color: hsl(var(--bg));
  color: hsl(var(--txt));
  display: grid;
  min-height: 300vh;
  max-width: 100vw;
  padding: 5vmax;
  place-items: center;
  font-family: 'League Spartan', sans-serif;
  overflow-x:hidden;

}

body:has(div > canvas){
  background-color: #000;
}

section{
}

canvas {
  object-fit: contain;
  max-height: 100%;
  max-width: 100%;

}

.hero-lightpass-parent{
  position: fixed;
  top: 0;
  right: 0;
  bottom: 0;
  left: 0;
  background-color: black;
  display: flex;
  justify-content: center;
  align-items: center;
}


::selection {
  background: hsl(var(--accent) / 0.8);
  color: hsl(var(--bg));
}



.container{
  margin-inline: max(calc((100vw - 70rem) / 2), 1.5rem);
  display: grid;
  gap: 1.5vmax;
  text-align: center;

}

form{
  display: grid;
  gap: .8em;
  max-width: calc(var(--_size)*20);
  font-size: var(--_size);
  text-align: left;
  padding-block: .5em;

}

.input-wrapper{
  position: relative;
  display: grid;
  gap: .2em;
  margin-block-start: .6em;

}

.nav{
  position: absolute;
  display: flex;
  text-align: center;
  gap: .2em;
  margin-block-start: .6em;
  left: 0;
  bottom: 0;
  flex-direction: row;
  padding: 2em;
}


.form-label{
  text-transform: uppercase;
  font-size: .7em;
  letter-spacing: 0.05em;
  margin-inline: 0.45em;
  position: absolute;
  top: 50%;
  transform: translateY(-50%);
  padding: .1em .35em;
  background-color: hsl(var(--muted));
  transition: transform var(--_tspeed_fast) var(--_ttype_squish), background-color var(--_tspeed_fast) var(--_ttype_squish);
}

.form-input {
  border:none;
  border-radius: var(--_radius);
  padding: 0.35em 0.55em;
  width: 100%;
  background-color: hsl(var(--muted));
  caret-color: hsl(var(--accent));
  box-shadow: 0 0 0 -.1em hsl(var(--bg)),
  0 0 0 .2em hsl(var(--accent)/ .8);
  transition: box-shadow var(--_tspeed_slow) var(--_ttype_squish);

}

.form-input:focus{
  outline: none;
  box-shadow: 0 0 0 0.2em hsl(var(--bg)),
  0 0 0 0.4em hsl(var(--accent)/ .8);
}

.form-input:focus ~ .form-label, .form-input:not(:placeholder-shown) ~ .form-label {
  transform: translate3d(0, -2.7em, 0);
  background-color: hsl(var(--bg));
  color: hsl(var(--accent) / .8);
}

.form-input::placeholder{
  opacity: 0;
}

@media screen and (min-width: 600px){
  .md\:span-2 {
    grid-column: 1 / span 2;
  }
}


.btn {
  background-color: hsl(var(--accent));
  color: hsl(var(--bg));
  text-decoration: none;
  border: none;
  font-size: calc(var(--_size)*1.2);
  font-weight: 700;
  margin-block: calc(var(--_size));
  padding: 0.4em 1.4em;
  box-shadow: 0.05em 0.1em 0.9em hsl(var(--accent) / 0.3),
  0 0 0 -0.1em hsl(var(--bg)), 0 0 0 -0.2em hsl(var(--accent));
  transition: box-shadow var(--_tspeed_slow) var(--_ttype_squish),
  background-color var(--_tspeed_slow) var(--_ttype_squish);
}

.btn :where(svg, img, span) {
  pointer-events: none;
}

.btn :where(svg, img) {
  width: var(--_size);
}

.btn:where(:active, :hover) {
  background-color: hsl(var(--accent) / 0.7);
  box-shadow: 0 0 0 hsl(var(--accent) / 0.3), 0 0 0 -0.1em hsl(var(--bg)),
  0 0 0 -0.2em hsl(var(--accent));
}

.btn:focus {
  outline: none;
}

.btn:focus-visible {
  box-shadow: 0 0 0 hsl(var(--accent) / 0.3), 0 0 0 0.2em hsl(var(--bg)),
  0 0 0 0.4em hsl(var(--accent) / 0.7);
}



</style>


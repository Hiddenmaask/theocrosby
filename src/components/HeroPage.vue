<template>
  <section>
    <div class="info">
      <div>
        <h1>
          This is Theo Crosby.
        </h1>
        <h2>
          Yes, that's right. It's really him.
        </h2>
        <div style="display: inline-flex">
          <input type="button" class="btn" value="Contact Me">
          <h3 >Recommended by everyone</h3>
        </div>
      </div>
      <div class="image">
        <div class="circle">
        </div>
        <div class="circle">
        </div>
        <img alt="Vue logo"  src="@/assets/theo2.png">
      </div>
    </div>
  </section>

</template>

<script>
export default {
  name: "HeroPage"
}
</script>

<style scoped>

section{
  min-height: 100vh;

}

h1{
  font-style: normal;
  font-weight: 700;
  font-size: calc(var(--_size)*2);
  line-height: 59px;
}

h2{
  font-style: normal;
  font-weight: 400;
  font-size: calc(var(--_size)*1.2);
  line-height: 85px;
}

h3{
  align-self: center;
  font-style: normal;
  font-weight: 400;
  font-size: 40px;
  line-height: 37px;
  font-size: calc(var(--_size)*1);
  color: hsl(var(--accent));
  padding-left: calc(var(--_size)/2) ;

}

.info{
  padding-block: 10%;
  width: 100%;
  max-height: 100%;
  display: grid;
  grid-template-columns: 1fr 1fr;

}

.image{
  max-width: 100%;
  position: relative;
  margin-left: auto;

}
img{
  width: 40vw;
  height: auto;
}

.circle:nth-child(1){
  height: calc(var(--_size)*9);
  width: calc(var(--_size)*9);
  border-radius: 100vmax;
  position: absolute;
  background: hsl(var(--accentalt));
  z-index: 4;
  right:-30%;
  bottom: -30%;

}

.circle:nth-child(2){
  height: calc(var(--_size)*7);
  width: calc(var(--_size)*7);
  border-radius: 100vmax;
  position: absolute;
  background: hsl(var(--accent)/0.60);
  backdrop-filter: blur(5px);
  z-index: 4;
  left:10%;
  top: -20%;

}


</style>

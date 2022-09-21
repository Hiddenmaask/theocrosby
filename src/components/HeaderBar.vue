<template>
  <ul class="header">

    <a>
      home
    </a>
    <a>
      find me
    </a>
    <a>
      socials
    </a>
    <a>
      contact
    </a>

  </ul>

</template>

<script>
export default {
  name: "HeaderBar"
}
</script>

<style scoped>
.header{
  /*Opacity start*/
  background: hsl(var(--bg));
  background-size: cover;
  background-position: center;
  -ms-filter: "progid:DXImageTransform.Microsoft.Alpha(Opacity=50)";
  filter: alpha(opacity=80);
  -moz-opacity: 0.80;
  -khtml-opacity: 0.8;
  opacity: 0.8;
  /*Opacity end*/
  position: fixed;
  top: 0;
  width: 90%;
  height: calc(var(--_size)*2);
  border-bottom: 2px solid hsl(var(--accentalt)) ;
  z-index: 5;



  display: grid;
  grid-template-columns: 4fr 1fr 1fr 1fr;
  justify-content: space-around;
  grid-gap: var(--_size);
  align-items: end;


}




li{
  display: inline;
}
.home{

}

ul a{
  display: block;
  padding: 8px;
  color: var(--accentalt);
  font-style: normal;
  font-weight: 400;
  font-size: calc(var(--_size)*1.2);

}


ul {
  list-style-type: none;
  padding: 0;
  margin: 0;
}

a:not(:first-child){
  direction: rtl;
}

</style>

<template>
  <Nav />
  <main>
    <slot />
  </main>
  <Footer />
</template>
  
  <style>
body {
  margin: 0;
  padding: 0;
}

html {
  height: 100%;
  width: 100%;
  background-color: white;
  overflow-x: hidden;
}

nav {
  width: 100%;
  height: 120px;
  background-color: white;
}

/* Global Font opsat korrekt her til alt content for nu */
* {
  font-family: "Opel Sans Regular", fallback-font, sans-serif;
}

h1 {
  font-size: 64px;
  font-weight: bold;
}

h2 {
  font-size: 48px;
  font-weight: bold;
}

h4 {
  font-size: 34px;
  font-weight: 600;
}

h5 {
  font-size: 23px;
  font-weight: 600;
}

h3 {
  font-size: 34px;
  font-weight: 650;
}

a {
  font-size: 19px;
}

p {
  font-size: 24px;
  font-weight: medium;
}

@media only screen and (max-width: 767px) {
  h2 {
    font-size: 32px;
    font-weight: bold;
    min-width: 320px;
  }

  h1 {
    font-size: 54px;
    font-weight: bold;
  }

  h4 {
    font-size: 38px;
    font-weight: 600;
  }

  h5 {
    font-size: 23px;
    font-weight: 600;
  }

  h3 {
    font-size: 34px;
    font-weight: 650;
  }

  a {
    font-size: 18px;
  }

  p {
    font-size: 20px;
    font-weight: 600;
    min-width: 280px;
  }
}

/* Fontfaces indsat i layout og kan bruges på alle sider, linket til Default Nuxt static mappe 'public' (Her er fonts placeret) */
@font-face {
  font-family: "Opel Sans Bold";
  src: url("fonts/Opel-Sans-Bold.ttf") format("truetype");
  font-weight: bold;
  font-style: normal;
}

@font-face {
  font-family: "Opel Sans Bold Italic";
  src: url("fonts/Opel-Sans-Bold-Italic.ttf") format("truetype");
  font-weight: bold;
  font-style: italic;
}

@font-face {
  font-family: "Opel Sans Italic";
  src: url("fonts/Opel-Sans-Italic.ttf") format("truetype");
  font-weight: normal;
  font-style: italic;
}

@font-face {
  font-family: "Opel Sans Regular";
  src: url("fonts/Opel-Sans-Regular.ttf") format("truetype");
  font-weight: normal;
  font-style: normal;
}
</style>
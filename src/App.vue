<template>
  <div class="app">
    <header>
      <router-link to="/">
        <h1><span>DISCOVER: </span>Movies</h1>
      </router-link>
    </header>
    <main>
      <router-view />
    </main>
  </div>
</template>

<style>
@import url('https://fonts.googleapis.com/css2?family=Poppins:wght@100;200;300;400;500;600;700;800;900&display=swap');

* {
  padding: 0;
  margin: 0;
  box-sizing: border-box;
  font-family: 'poppins', sans-serif;
}
body {
  background-color: black;
  color: #fff;
}


a {
  text-decoration: none;
}

header {
  display: flex;
  align-items: center;
  justify-content: flex-start;
  padding: 10px 16px;
  background-color: #000000;
}

header h1 {
  color: #ffffff;
  font-size: 28px;
}

header h1 span {
  letter-spacing: 5px;
}

</style>

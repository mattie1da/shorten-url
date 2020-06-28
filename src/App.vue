<template>
  <div id="app">
    <div class="container">
      <Title/>
      <ShortenForm/>
    </div>
  </div>
</template>

<script>
import Title from './components/Title';
import ShortenForm from './components/ShortenForm';

export default {
    name: 'App',

    components: {
        Title,
        ShortenForm
    },
}
</script>

<style lang="scss">
  :root {
    --colour-bg: 0, 0, 0;
    --colour-white: white;
    --colour-yellow: yellow;
    --colour-title: 255, 255, 255;
    --colour-error: #ffb37c;
    --theme: linear-gradient(90deg, #1e24ec, #8d1aff);
    --font: 'Krona One', sans-serif;
  }

  body {
    color: var(--colour-white);
    margin: 0;
    padding: 0;
    font-family: var(--font);

    ::selection {
      background: var(--colour-yellow);
      color: black;
    }
  }

  a {
    color: inherit;
    text-decoration: none;
  }

  h1 {
    margin: 0;
  }

  .container {
    background: rgba(var(--colour-bg), 1);
    display: flex;
    flex-direction: column;
    justify-content: center;
    min-height: 100vh;
    padding: 0 1rem;

    @media (min-width: 750px) {
      align-items: center;
      padding: 1rem;
    }
  }

  .highlight {
    position: relative;
    z-index: 1;

    &:after {
      background: var(--theme);
      bottom: 0;
      content: '';
      left: 0;
      position: absolute;
      right: 0;
      top: 0;
      transform: skew(-5deg) rotate(-2deg);
      z-index: -1;
    }
  }

  .link {
    text-decoration: underline;
  }

</style>

<template>
    <div>
        <div class="title-wrapper">
            <h1 class="title"><a href="/"><span class="highlight">shorten</span>;</a></h1>
            <Help/>
        </div>
        <p class="subtitle">paste in any url ✨</p>
    </div>
</template>

<script>
import Help from '../components/Help'

export default {
    name: "Title",

    components: {
        Help
    }
}
</script>

<style scoped lang="scss">
    .title-wrapper {
        margin-bottom: 0.3rem;
        position: relative;
        text-align: center;
    }

    .title {
        color: var(--colour-white);
        font-size: 10vw;
        font-weight: 600;

        @media (min-width: 750px) {
            font-size: 4vw
        }
    }

    .subtitle {
        color: rgba(var(--colour-title), 0.9);
        margin: 0 0 3rem 0;
        text-align: center;
    }
</style>
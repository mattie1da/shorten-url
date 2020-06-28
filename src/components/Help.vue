<template>
    <div>
        <a href="#" @click.prevent="needHelp = true" class="help">
            ?
        </a>
        <div v-if="needHelp == true" class="help__content">
            <p>this is built utilising an api from <a href="https://rel.ink/" class="highlight link" target="_blank">https://rel.ink</a></p>
            <p>simply paste in any url from your browser into the form provided. <br>when submitted, you'll see the shorter version.</p>
            <p>you can copy your shiny new url directly to your clipboard by clicking the clipboard icon.</p>
            <p>built by <a href="https://mattie.world" target="_blank" class="link highlight">mattie1da</a></p>
            <a href="#" @click.prevent="needHelp = false" class="help__close">x</a>
        </div>
    </div>
</template>

<script>
export default {
    name: "Help",

    data() {
        return {
            needHelp: false,
        }
    }
}
</script>

<style scoped lang="scss">
    .help {
        align-items: center;
        background: var(--theme);
        border-radius: 50%;
        display: flex;
        font-size: 0.75rem;
        height: 30px;
        justify-content: center;
        position: absolute;
        right: 5vw;
        text-decoration: none;
        top: 0;
        width: 30px;

        @media (min-width: 750px) {
            height: 20px;
            right: -1rem;
            top: -1rem;
            transition: 200ms ease-in-out;
            width: 20px;

            &:hover {
                transform: translateY(-.1rem);
            }
        }
    }

    .help__content {
        background: black;
        border-radius: .5rem;
        font-size: 0.75rem;
        max-width: 200px;
        padding: .5rem 3rem;
        position: absolute;
        right: 1rem;
        text-align: left;
        top: -1rem;
        width: 100%;
        z-index: 2;

        @media (min-width: 750px) {
            top: -2rem;
            transform: translateX(100%);
            right: 1rem;
        }
    }

    .help__close {
        color: white;
        text-decoration: none;
        font-size: 1rem;
        position: absolute;
        right: 1rem;
        top: 1rem;

        @media (min-width: 750px) {
            left: 1rem;
            right: auto;
        }
    }
</style>
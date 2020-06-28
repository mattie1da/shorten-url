<template>
    <footer class="signature">
        <a href="https://github.com/mattie1da/shorten-url" class="link signature__sauce" target="_blank">view the sauce</a>
        <p>by <a href="https://mattie.world" class="link signature__boi" target="_blank">mattie1da</a></p>
    </footer>
</template>

<script>
export default {
    name: "Signature"
}
</script>

<style scoped lang="scss">
    .signature {
        display: none;

        @media (min-width: 750px) {
            bottom: 2vw;
            color: rgba(var(--colour-title), 0.6);
            display: flex;
            font-size: .4rem;
            position: absolute;
            right: 2vw;
            text-align: right;

            p, a {
                margin: 0;
            }
        }

        .signature__sauce {
            margin-right: .5rem;
        }
    }
</style>
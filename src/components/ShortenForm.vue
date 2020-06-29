<template>
    <div>
        <form class="form">
            <label class="form__label" for="url">paste your url ⬇️</label>
            <div class="form__item">
                <input class="form__input" placeholder="feed me" v-model="url" id="url" name="url" type="url">
                <button @click.prevent="shorten" class="form__button" type="submit">send</button>
            </div>
            <p class="form__error" v-if="hasErrors">
                {{ error }}
            </p>
        </form>

        <div v-if="results.length" class="results">
            <p v-for="(result, index) in results" v-bind:key="result[index]" class="result">
                <span class="old-result">{{ result.old }} </span> ✨<a :href="result.new" class="link highlight" target="_blank">{{ result.new }}</a>
                <a href="#" @click.prevent="selectResult(index)" class="result__clipboard" :class="{ 'result__clipboard--active' : index === activeResult }" v-clipboard:copy="result.new">
                    <svg xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" aria-hidden="true" focusable="false" width="1em" height="1em" style="-ms-transform: rotate(360deg); -webkit-transform: rotate(360deg); transform: rotate(360deg);" preserveAspectRatio="xMidYMid meet" viewBox="0 0 1792 1792"><path d="M768 1664h896v-640h-416q-40 0-68-28t-28-68V512H768v1152zm256-1440v-64q0-13-9.5-22.5T992 128H288q-13 0-22.5 9.5T256 160v64q0 13 9.5 22.5T288 256h704q13 0 22.5-9.5t9.5-22.5zm256 672h299l-299-299v299zm512 128v672q0 40-28 68t-68 28H736q-40 0-68-28t-28-68v-160H96q-40 0-68-28t-28-68V96q0-40 28-68T96 0h1088q40 0 68 28t28 68v328q21 13 36 28l408 408q28 28 48 76t20 88z" fill="white"/></svg>
                </a>
                <a href="#" @click.prevent="removeResult(index)" class="result__remove">
                    x
                </a>
                <span class="notice" :class="{ 'notice--active' : index === activeResult }" v-if="copiedUrl = true">URL copied to clipboard!</span>
            </p>
        </div>
    </div>
</template>

<script>
import axios from 'axios';

export default {
    name: "ShortenForm",

    data() {
        return {
            url: '',
            hasErrors: false,
            apiResult: '',
            results: [],
            copiedUrl: false,
            activeResult: null,
            error: ''
        }
    },

    methods: {
        shorten() {
            // improve this validation. hasErrors as it's own function?
            if (this.url == '') {
                this.hasErrors = true;
                this.error = '*insert a url'
            } else if (!this.url.includes('https://' || 'http://')) {
                this.hasErrors = true;
                this.error = 'include https:// at the beginning'
            } else {
                this.hasErrors = false;
                axios
                    .post('https://rel.ink/api/links/', { url: this.url })
                    .then(response => (
                        this.apiResult = this.apiResult + 'https://rel.ink/' + response.data.hashid,

                        this.results.push({
                            new: this.apiResult,
                            old: this.url,
                        }),

                        this.url = '',
                        this.apiResult = '',
                        this.hasErrors = false
                    )
                )
            }
        },

        selectResult(index) {
            this.activeResult = index;
            this.copiedUrl = !this.copiedUrl;
        },

        removeResult(index) {
            this.results.splice(index, 1);
        }
    }
}
</script>

<style scoped lang="scss">
    .form {
        display: block;

        @media (min-width: 750px) {
            display: grid;
            justify-content: center;
        }
    }

    .form__label {
        display: block;
        padding-left: 1rem;
        margin-bottom: .5rem;
    }

    .form__item {
        border: 2px solid black;
        border-radius: 1rem;
        display: flex;
        flex-direction: column;
        overflow: hidden;
        position: relative;
        width: 100%;

        @media (min-width: 750px) {
            border-radius: 2rem;
            flex-direction: row;
            width: 500px;
        }
    }

    .form__input {
        font: 10px var(--font);
        padding: 1rem;
        border: none;
        width: 100%;

        &:focus {
            outline: none;
        }
    }

    ::placeholder {
        color: grey;
    }

    .form__error {
        color: var(--colour-error);
        font-size: 0.75rem;
        grid-column: 1 / -1;
        padding-left: 1rem;
    }

    .form__button {
        background: var(--theme);
        border: none;
        color: var(--colour-white);
        cursor: pointer;
        font: inherit;
        position: static;
        padding: .5rem;

        @media (min-width: 750px) {
            bottom: 0;
            padding: 0;
            position: absolute;
            right: 0;
            top: 0;
            width: 100px;
        }
    }

    .results {
        margin-top: 2rem;
        max-height: 350px;
        overflow-y: auto;
    }

    .result {
        align-items: center;
        display: flex;
        justify-content: center;

        @media (min-width: 750px) {
            justify-content: flex-end;
            position: relative;

            &:hover {
                .result__remove {
                    visibility: visible;
                    opacity: 1;
                }
            }
        }
    }

    /*rename*/
    .old-result {
        display: none;

        @media (min-width: 750px) {
            color: rgba(var(--colour-title), 0.5);
            display: inline-block;
            max-width: 333px;
            text-decoration: line-through;
            text-overflow: ellipsis;
            overflow: hidden;
            white-space: nowrap;
        }
    }

    .result__clipboard {
        display: none;

        @media (min-width: 750px) {
            cursor: pointer;
            display: block;
            margin-left: .75rem;

            &:hover,
            &--active {
                path {
                    fill:var(--colour-yellow);
                }
            }
        }
    }

    .result__remove {
        display: none;

        @media (min-width: 750px) {
            color: rgba(var(--colour-title), 0.8);
            display: block;
            font-size: .8rem;
            line-height: 1;
            margin-left: .75rem;
            margin-top: -4px;
            opacity: 0;
            visibility: hidden;

            &:hover {
                color: var(--colour-error);
            }
        }
    }

    .notice {
        display: none;

        @media (min-width: 750px) {
            background: var(--colour-yellow);
            bottom: 0;
            color: black;
            display: block;
            font-size: 0.8rem;
            padding: 1rem;
            position: absolute;
            right: 0;
            opacity: 0;
            visibility: hidden;
            z-index: 2;

            &--active {
                animation: fadeOut 1s;
            }
        }
    }

    @keyframes fadeOut {
        0% {
            opacity:0.9;
            visibility: visible;
        }
        80% {
            opacity: 0.9;
        }
        100% {
            opacity:0;
            visibility: hidden;
        }
    }
</style>
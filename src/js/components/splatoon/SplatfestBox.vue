<template>
    <div class="font-splatoon2">
        <div class="splatfest-header">
            <h2 class="title is-3 is-size-2-fullhd font-splatoon1">
                Splatfest
            </h2>
        </div>

        <div class="panel-container">
            <div class="image">
                <img :src="image" />
            </div>
            <div class="alpha">
                {{ festival.names.alpha_short }}
            </div>
            <div class="bravo">
                {{ festival.names.bravo_short }}
            </div>
        </div>

        <div class="has-text-centered is-size-5 title-color festival-period-container">
            <span class="festival-period" :style="{ 'background-color': festival.colors.middle.css_rgb }">
                {{ festival.times.start | date }}
                {{ festival.times.start | time }}
                &ndash;
                {{ festival.times.end | date }}
                {{ festival.times.end | time }}
            </span>
        </div>

        <div class="splatfest-content has-text-centered">
            <template v-if="festival.times.start <= now">
                {{ festival.times.end - now | duration }}
                remaining
            </template>
            <template v-else>
                in
                {{ festival.times.start - now | duration }}
            </template>
        </div>
    </div>
</template>

<script>
export default {
    props: ['festival', 'now'],
    computed: {
        image() {
            if (this.festival)
                return `https://app.splatoon2.nintendo.net${this.festival.images.panel}`;
        }
    }
}
</script>
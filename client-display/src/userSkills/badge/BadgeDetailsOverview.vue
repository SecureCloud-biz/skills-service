<template>
    <div class="row">
        <div class="col-lg-2">
            <div class="card mb-2">
                <div class="card-body">
                    <i :class="badge.iconClass" class="text-success fa-3x" style="min-width: 3rem;, max-width: 4rem;"/>
                    <i v-if="badge.gem" class="fas fa-gem position-absolute" style="top: 5px; right: 5px; color: purple"></i>
                    <div v-if="badge.gem" class="text-muted">
                        <small>Expires {{ badge.endDate | moment("from", "now") }}</small>
                    </div>
                </div>
            </div>
        </div>

        <div class="text-sm-left text-center catalog-item col-lg-10">
            <div class="row">
                <h4 class="mb-1 col-md-8">{{ badge.badge }}</h4>
                <div class="col-md-4 text-right">
                    <small class=" float-right text-navy" :class="{ 'text-success': percent === 100 }">
                        <i v-if="percent === 100" class="fa fa-check"/> {{ percent }}% Complete
                    </small>
                </div>
            </div>


            <div class="mb-2">
                <progress-bar bar-color="lightgreen" :val="percent"></progress-bar>
            </div>

            <p class="">
                {{ badge.description }}
            </p>


            <slot name="body-footer" v-bind:props="badge">

            </slot>

<!--            <router-link :to="{ name: 'badgeDetails', params: { badgeId: badge.badgeId }}" tag="button" class="btn btn-info btn-sm mr-1 text-uppercase">-->
<!--                View Details-->
<!--            </router-link>-->
        </div>
    </div>
</template>

<script>
    import ProgressBar from 'vue-simple-progress';

    export default {
        name: 'BadgeDetailsOverview',
        components: {
            ProgressBar,
        },
        props: {
            badge: {
                type: Object,
                required: true,
            },
        },
        computed: {
            percent() {
                return Math.trunc((this.badge.numSkillsAchieved / this.badge.numTotalSkills) * 100);
            },
        },
    };
</script>

<style scoped>
    .catalog-item {
        font-size: 0.8rem;
        font-weight: 400;
        line-height: 1.5;
        color: #4f565d;
    }
</style>
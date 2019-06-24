<template>
    <div>
        <div
            class="selected__image"
            :class="filterName"
            :style="{backgroundImage: 'url(' + baseImg + ')'}"
        ></div>
        <div class="filter__container" v-dragscroll>
            <div class="filter__type"
              :key="filter.name"
              v-for="(filter,index) in filters"
            >
                <p>{{ filter.name }}</p>
                <div
                    class="img"
                    :class="filter.name"
                    :style="{backgroundImage: 'url(' + baseImg + ')'}"
                    @click="selectFilter(index)"
                ></div>
            </div>
        </div>
    </div>
</template>

<script>
import eventBus from '../event-bus.js';
export default {
    props: {
        filterName: {
            type: String
        },
        filters: {
            type: Array
        },
        baseImg: {
            type: String
        }
    },
    methods: {
        selectFilter(index) {
            eventBus.$emit('changeFilter', this.filters[index].name);
        }
    },
}
</script>

<style>

</style>

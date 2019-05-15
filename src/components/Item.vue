<template>
    <div v-if="picture">
        <div class="item">
            <a v-bind:href="picture.url" target="_blanck">
                <img v-bind:src="picture.img" alt="not fount">
            </a>
            <div class="desc">
                <span>description</span>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name:"Item",
    props:{
        picture: Object,

    }
    
}
</script>

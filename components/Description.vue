<template>

<section class="codeEvent">
    <div>
        <h4>{{this.title}}</h4>
        <p>{{this.text}}</p>
        <img class="children" v-bind:src="this.img">
    </div>
</section>

</template>

<script>
export default {
    props: {
        title: String,
        text: String,
        img: String
    }
}

</script>

<style scoped>

section {
    font-family: Arial, Helvetica, sans-serif;
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100vh;
}

section h4 {
    font-size: 35px;
}


section p {
    font-size: 20px;
}

img {
    height: 450px;
}

</style>
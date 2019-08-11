<template>
    <section class="codeEvent" :id="slug">
        <div>
            <h4>{{title}}</h4>
            <p>{{text}}</p>
            <img class="children" v-bind:src="img">
        </div>
    </section>
</template>

<script>
export default {
    props: {
        title: String,
        text: String,
        img: String,
        slug: String,
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
<template>
    <section class="content" :id="slug">
        <div class="content-body">
            <div class="content-text">
                <h2>{{title}}</h2>
                <p>{{text}}</p>
            </div>
            <img :src="img">
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
    display: flex; 
    align-items: center; 
    justify-content: center; 
    margin: auto; 
    height: 70vh;
    max-width: 80vw; 
}

.content:nth-child(2) .content-body {
  flex-direction: row-reverse; 
}

.content-body {
    display: flex;
    flex-direction: row; 
    justify-content: center;
    align-items: center;
    width: 100%; 
}

.content-text {
    align-self: flex-start
}

.content-text p {
    max-width: 32em;
}

h2 {
    font-size: 2.1em;
    margin-bottom: 8px;
    align-self: center;
}

img {
    max-height: 300px;
    box-shadow: 0 16px 32px -3px rgba(0, 0, 0, 0.2), 0 4px 6px -2px rgba(0, 0, 0, 0.2);
    border-radius: 4px; 
    margin-left: 32px; 
    margin-right: 32px;
    align-self: flex-end;
}

@media (max-width: 59em) {
    .content {
        margin-bottom: 64px;
    }

    section.content div.content-body,
    section.content:nth-child(2) div.content-body {
        flex-direction: column; 
    }

    .content .content-body img {
        margin-top: 32px;
        align-self: center;
    }
}
</style>
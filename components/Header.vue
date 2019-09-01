<template>
<header>
    <!--Overlay over de header-->
    <div id="overlay"></div>

    <!--Header-->
    <nav>
        <ul class="navbar" :class="{pastHeader: isNavbarPastHeader}">
            <li v-for="navitem of navitems"
                :key="navitems.indexOf(navitem)"
                >
                  <a :href="'#' + navitem.slug">{{ navitem.title }}</a>
            </li>
        </ul>
    </nav>

    <div id="header" :style="{backgroundImage: 'url(' + img + ')'}">
        <div id="headertext">
            <h1>
                {{ title }}
            </h1>
        </div>
    </div>

</header>
</template>
<script>
export default {
    props: {
        title: String,
        navitems: {
            type: Array,
            validator: function (navitems) {
                for(let navitem of navitems) {
                    if (!navitem.title && navitem.slug) {
                        return false
                    }
                }

                return true
            }
        },
        img: String,
    },
    data() {
        return {
            isNavbarPastHeader: false, 
        }
    },
    mounted() {
        if(!'IntersectionObserver' in window) {
          this.$data.isNavbarPastHeader = true
          return
        }

        let observer = new IntersectionObserver((entries, observer) => {
            let navbar = entries[0]
            let isPastHeader = !navbar.intersectionRatio
            this.$data.isNavbarPastHeader = isPastHeader
        }, {thresholds: [0.0, 1.0]})

        observer.observe(document.getElementById('header'))
    }
}
</script>

<style scoped>
header{
    display: flex;
    justify-content: center;
}

#header{
    width: 100vw;
    height: 100vh;
    color: white;
    background-position: center center;
    background-size: cover;
    background-repeat: no-repeat;  
}

#headertext{
    display: flex;
    justify-content: center;
    align-items:center;
    width: 100%;
    height: 100vh;
}

#overlay{
    background-image: linear-gradient(160deg, rgba(0,0,0,0.1), rgba(0,0,0,0.4), rgba(0,0,0,0.1));
    height: 100vh;
    width: 100%;   
    position: absolute;
    z-index: 0;
}

h1{
    z-index: 0;
    font-size: 2.5em;
    font-weight: unset; 
}

nav, .navbar{
    display:flex;
    position:fixed;
    justify-content:center;
    list-style-type:none;
    z-index: 1;
    padding:0px;
    width: 100vw; 
}

.navbar {
    transition: all 0.2s; 
    padding: 12px;
}

.navbar.pastHeader {
    transition: all 0.2s; 
    background: #cf1046;
    box-shadow: 0 10px 15px -3px rgba(0, 0, 0, 0.1), 0 4px 6px -2px rgba(0, 0, 0, 0.05);
}

a:hover{
   border-bottom: solid;
   border-style: black;
}

li a{
    margin: 20px;
    color: white;
    text-decoration: none;
    width: fit-content;
    transition: all 0.3s; 
    text-transform: capitalize;
}

@media screen and (max-width: 400px) {
    .navbar{
        display: inline;
        list-style-type:none;
        z-index: 1;
        text-align:center;
    }
  }
</style>

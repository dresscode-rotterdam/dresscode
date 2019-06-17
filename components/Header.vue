<template>

<header>
    <!--Overlay over de header-->
    <div id="overlay">
        
    </div>

    <!--Header-->
    <nav>
        <ul class="navbar">
            <li><a href="#">Home</a></li>
            <li><a href="#">Wie zijn wij?</a></li>
            <li><a href="#">Aanmelden</a></li>
        </ul>
    </nav>

    <div id="header">
        <div id="headertext">
            <h1>
                Hey!
            </h1>
        </div>
    </div>

</header>
</template>

<style scoped>
body{
    margin: 0;

}

header{
    display:flex;
    justify-content:center;
}

#header{
    width: 100vw;
    height: 100vh;
    background-image: url("https://images.pexels.com/photos/4700/nature-forest-moss-leaves.jpg?auto=compress&cs=tinysrgb&dpr=2&h=750&w=1260");
    color: white;
    font-family: arial;
    font-size: 8vw;
    
}

#headertext{
    display: flex;
    justify-content: center;
    align-items:center;
    width: 100%;
    height: 100vh;
}

#overlay{
    background-image: linear-gradient(to bottom, rgba(0,0,0,0), rgba(0,0,0,1));
    height: 100vh;
    width: 100%;   
    position:absolute;
    z-index: 0;
}

h1{
    z-index: 1;
}

nav, .navbar{
    display:flex;
    position:fixed;
    justify-content:center;
    font-size:30px;
    list-style-type:none;
    z-index: 1;
    font-family:arial;
    padding:0px;
}

a:hover{
   border-bottom: solid;
   border-style: black;
}

li a{
    padding: 20px;
    color: white;
    text-decoration: none;
    width: fit-content;
}

@media screen and (max-width: 400px) {
    .navbar{
        display: inline;
        font-size:30px;
        list-style-type:none;
        z-index: 1;
        font-family:arial;
        text-align:center;
    }
  }
  
</style>

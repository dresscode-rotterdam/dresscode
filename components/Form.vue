<template>
    <form>
        <h1>Meld je aan voor de introductie</h1>
        <input type="text" name="firstname" placeholder="Voornaam" aria-label="Voornaam" required>
        <input type="text" name="prefix" placeholder="Tussenvoegsel" aria-label="Tussenvoegsel">
        <input type="text" name="lastname" placeholder="Achternaam" aria-label="Achternaam" required>
        <input type="number" name="studentnumber" placeholder="Studentennummer" aria-label="studentennummer" min="1000000" required>
        <select name="bachelor" aria-label="Opleiding" required>
            <option value="">Opleiding</option>
            <option value="ti">Technische Informatica</option>
            <option value="inf">Informatica</option>
            <option value="cmgt">Creative Media and Game Technologies</option>
            <option value="other">Overig</option>
        </select>
        <input type="submit" value="Aanmelden">
    </form>
</template>

<style scoped>
form {
    display: flex; 
    flex-direction: column;
    max-width: 500px;
    padding: 24px;
    border-radius: 8px; 
    box-shadow: 0 10px 15px -3px rgba(0, 0, 0, 0.1), 0 4px 6px -2px rgba(0, 0, 0, 0.05);
}

h1 {
    font-size: 2em;
    text-align: center;
    margin-left: 16px;
    margin-right: 16px;
}

input, select {
    margin-top: 16px;
    height: 40px;
    width: 100%;
    padding: 8px;
    background-color: #f5f5f5;
    border-radius: 8px;    
    
}

select {
    appearance: none;
    background-image: url('/drop-down-arrow.png');
    background-position: 98%;
    background-repeat: no-repeat;
    background-size: 2%; 
}

input[type="submit"] {
    background-color: #cf1046;
    color: #ffffff;
}

input[type="number"] {
    -moz-appearance: textfield;
}

input[type="number"]::-webkit-inner-spin-button, 
input[type="number"]::-webkit-outer-spin-button {
    appearance: none;
}
</style>

<template>
    <form
        :name="name"
        method="POST"
        @submit.prevent="submitHandler"
    >
        <h1>{{ this.title }}</h1>
        <input type="text" name="firstname" v-model="inputValues.firstname" placeholder="Voornaam" aria-label="Voornaam" required>
        <input type="text" name="prefix" v-model="inputValues.prefix" placeholder="Tussenvoegsel" aria-label="Tussenvoegsel">
        <input type="text" name="lastname" v-model="inputValues.lastname" placeholder="Achternaam" aria-label="Achternaam" required>
        <input type="number" name="studentnumber" v-model="inputValues.studentnumber" placeholder="Studentennummer" aria-label="studentennummer" min="99999" required> 
        <select name="bachelor" v-model="inputValues.bachelor" aria-label="Opleiding" required>
            <option value="">Opleiding</option>
            <option value="ti">Technische Informatica</option>
            <option value="inf">Informatica</option>
            <option value="cmgt">Creative Media and Game Technologies</option>
            <option value="other">Overig</option>
        </select>
        <input type="submit"/>
    </form>
</template>

<script>
export default {
    props: {
        title: String
    },
    data() {
        return {
            name: 'inschrijven-dresscode',
            inputValues: {
                firstname: '',
                prefix: '',
                lastname: '',
                studentNumber: '',
                bachelor: '', 
            }
            
        }
    },
    methods: {
        parse() {
            let data = {
                'form-name': this.name
            }

            for(let key in this.inputValues) {
                let value = this.inputValues[key]

                if(value) {
                    data[key] = value
                }
            }
            return data
        },

        encode(data) {
        return Object.keys(data)
                     .map((key) => encodeURIComponent(key) + '=' + encodeURIComponent(data[key]))
                     .join("&")
        },

        submitHandler(e) {
            let data = this.encode(this.parse())

            let headers = new Headers({
                'Content-Type': 'application/x-www-form-urlencoded',
                'Accept': 'application/x-www-form-urlencoded',
            })

            fetch('/#form', {
                headers: headers,
                body: data,
                method: 'POST'
            })
            .then((res) => {
                console.log('[sucesss]', res)
            })
            .catch((err) => {
                console.error('[error]', err)
            })
        },
    }

}
</script>

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

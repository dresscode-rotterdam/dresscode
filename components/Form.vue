<template>
    <form
        :name="name"
        method="POST"
        data-netlify="true"
        @submit.prevent="submitHandler"
    >
        <h1>{{ this.title }}</h1>
        <fieldset :disabled="submitValues.isDisabled">
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
            <div class="submit-container" ref="submit-container">
                <input type="submit" :value="submitValues.text">
                <span v-if="submitValues.icon">
                    <img :src="submitValues.icon" :alt="submitValues.iconAlt" :class="{spin: submitValues.spin}" />
                </span>
            </div>
        </fieldset>
        <p v-if="message" >{{ message }}</p>
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
            },
            submitValues: {
                text: 'Aanmelden',
                icon: '',
                iconAlt: '',
                spin: false,
                isDisabled: false,
            },
            message: ''
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
            this.submitValues.text = ' '
            this.submitValues.icon = '/icons/spinner-solid.svg'
            this.submitValues.iconAlt = 'Aanmelding aan het verzenden'
            this.submitValues.spin = true
            this.submitValues.isDisabled = true

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
                this.submitValues.icon = '/icons/check-solid.svg'
                this.submitValues.iconAlt = 'Aanmelding succesvol'
                this.submitValues.spin = false
                this.message = 'Bedankt voor het aanmelden!'
            })
            .catch((err) => {
                this.submitValues.icon = '/icons/times-solid.svg'
                this.submitValues.iconAlt = 'Aanmelding mislukt, refresh om het opnieuw te proberen'
                this.submitValues.spin = false
                this.message = 'Oeps, er ging iets fout. Refresh en probeer het opnieuw.'
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
    background-image: url('/icons/drop-down-arrow.png');
    background-position: 98%;
    background-repeat: no-repeat;
    background-size: 2%; 
}

input[type="submit"] {
    background-color: #cf1046;
    color: #ffffff;
    cursor: pointer;
}

.submit-container {
    height: 56px;
}

.submit-container span {
    position: relative;
    top: -32px;
    left: calc(50% - 12.5px);
}

.submit-container span img {
    width: 25px;
    height: 25px;
}

.spin {
    animation: spin 1.5s linear infinite; 
}

@keyframes spin {
    from {
        transform: rotate(0deg)
    }

    to {
        transform: rotate(360deg)
    }
}

input[type="number"] {
    -moz-appearance: textfield;
}

input[type="number"]::-webkit-inner-spin-button, 
input[type="number"]::-webkit-outer-spin-button {
    appearance: none;
}

fieldset:disabled, 
input:disabled, 
select:disabled {
    cursor: not-allowed;
}

p {
    margin-top: 8px;
}
</style>

<script>
export default {
    render() {
        return null
    },

    data() {
        return {
            dressStyle: `
                font-size: 28px;
                color: #cf1046;
                text-transform: uppercase;
                letter-spacing: 20px;
            `,
            codeStyle: `
                font-size: 28px;
                text-transform: uppercase;
            `
        }
    },

    mounted() {
        console.log('%c{👗}%cdress%ccode', this.codeStyle, this.dressStyle, this.codeStyle)
    }
}
</script>

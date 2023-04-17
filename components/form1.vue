<template>
    <div>
        <form>
            <input type="text" name="email" v-model="email">
            <button @click="send">Send</button>
        </form>
    </div>
</template>

<script>
    import io from 'socket.io-client'
    export default {
        data() {
            return {
                email: ""
            }
        },
        mounted() {
            this.socket = io('http://localhost:3005')
            console.log('connected to server socket');
        },
        methods: {
            async send(event) {
                event.preventDefault();
                console.log(this.email);
                const { data } = await useFetch('http://localhost:3005', {
                    method: 'POST',
                    body: {'email': this.email}
                })
            }
        }
    }
</script>
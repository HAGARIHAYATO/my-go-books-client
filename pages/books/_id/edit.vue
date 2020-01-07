<template>
    <div>
        <b-field horizontal label="Title">
            <b-input
                type="text"
                class="input-string"
                name="title"
                v-model="title"
                placeholder="Please enter title"
            ></b-input>
        </b-field>
        <b-field horizontal label="ISBN">
            <b-input
                type="number"
                class="input-number"
                name="isbn"
                v-model="isbn"
                placeholder="Please enter isbn"
            ></b-input>
        </b-field>
        <b-field horizontal label="Description">
            <b-input
                type="textarea"
                class="input-text"
                name="description"
                v-model="description"
                maxlength="200"
                placeholder="Please enter description"
            ></b-input>
        </b-field>
        <b-field horizontal><!-- Label left empty for spacing -->
            <p class="control">
                <button class="button is-primary" @click="sendRequest">UPDATE</button>
            </p>
        </b-field>
        <image :src="'http://images-jp.amazon.com/images/P/' + isbn + '.09.MZZZZZZZ'">
    </div>
</template>
<script>

export default {
    async asyncData({ app ,route }) {
        const response = await app.$axios.$get(`https://my-go-app-259011.appspot.com/api/v1/books/${route.params.id}`);
        return {
            title: response.Title,
            isbn: response.ISBN,
            description: response.Description
        };
    },
    methods: {
        async sendRequest() {
            const res = await this.$axios.$put(`https://my-go-app-259011.appspot.com/api/v1/books/${this.$route.params.id}`, {
                title: this.title,
                isbn: this.isbn,
                description: this.description
            })
            .then((res) => {
                this.$router.push(`/books/${this.$route.params.id}`)
            })
            .catch(err => console.error(err))
        }
    }
}
</script>
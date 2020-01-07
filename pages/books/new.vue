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
                <button class="button is-primary" @click="sendRequest">CREATE</button>
            </p>
        </b-field>
        <image :src="'http://images-jp.amazon.com/images/P/' + isbn + '.09.MZZZZZZZ'">
    </div>
</template>
<script>

export default {
    data () {
        return {
            title: "",
            isbn: "",
            description: ""
        }
    },
    methods: {
        async sendRequest() {
            const res = await this.$axios.$post("https://my-go-app-259011.appspot.com/api/v1/books", {
                title: this.title,
                isbn: this.isbn,
                description: this.description
            })
            .then((res) => {
                console.log(res.ID)
                this.$router.push(`/books/${res.ID}`)
            })
            .catch(err => console.error(err))
        }
    }
}
</script>
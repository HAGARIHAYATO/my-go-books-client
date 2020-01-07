<template>
    <section class="section">
        <b-table
            :paginated="isPaginated"
            :per-page="10"
            :data="books"
            :columns="columns">
            <template slot-scope="props">
                <b-table-column field="ID">
                    {{ props.row.ID }}
                </b-table-column>
                <b-table-column field="Title">
                    <nuxt-link :to="URL + props.row.ID">{{ props.row.Title }}</nuxt-link>
                </b-table-column>
                <b-table-column field="ISBN">
                    {{ props.row.ISBN }}
                </b-table-column>
            </template>
        </b-table>
    </section>
</template>

<script>
export default {
    data() {
        return {
            books: [],
            URL: "/books/",
            isPaginated: true,
            columns: [
                {
                    field: 'ID',
                    label: 'ID',
                    width: '100',
                    searchable: true,
                },
                {
                    field: 'Title',
                    label: 'Title',
                    width: '200',
                    searchable: true,
                },
                {
                    field: 'ISBN',
                    label: 'ISBN',
                    width: '200',
                    searchable: true,
                }
            ]
        }
    },
    async asyncData({ app }) {
        const response = await app.$axios.$get('https://my-go-app-259011.appspot.com/api/v1/books');
        return { books: response };
    },
    mounted: function() {
        this.books.forEach(function(value) {
            value.CreatedAt
        })
    }
}
</script>
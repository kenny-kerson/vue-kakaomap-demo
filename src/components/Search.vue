<template>
    <div>
        <div class="md-layout">
            <div class="md-layout-item"></div>
            <div class="md-layout-item">
                <md-field>
                    <label>키워드</label>
                    <md-input v-model="search"
                              @keyup.enter="changeSearch"
                    ></md-input>
                    <md-button class="md-raised md-primary"
                               @click="changeSearch"
                               @keyup.enter="changeSearch"
                    >
                        검색
                    </md-button>
                </md-field>
            </div>
            <div class="md-layout-item"></div>
        </div>
    </div>
</template>

<script>
    export default {
        name: "Search"
    }
</script>

<style scoped>

</style>
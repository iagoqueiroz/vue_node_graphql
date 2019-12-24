<template>
    <div>
        <div id="slogan" class="text-center">
            <h1>NameGenerator</h1>
            <br>
            <h6 class="text-secondary">Gerador de nomes utilizando Vue.js, GraphQL e Node !</h6>
        </div>
        <DomainList></DomainList>
    </div>
</template>

<script>
import "bootstrap/dist/css/bootstrap.css"
import "font-awesome/css/font-awesome.css"
import DomainList from "./components/DomainList"

export default {
    name: 'app',
    components: {
        DomainList
    }
}
</script>

<style>
#slogan {
    margin: 30px 0;
}

#main {
    padding: 30px 0;
    background-color: #F1F1F1;
}
</style>

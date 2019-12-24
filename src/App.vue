<template>
    <div>
        <div id="slogan" class="text-center">
            <h1>NameGenerator</h1>
            <br>
            <h6 class="text-secondary">Gerador de nomes utilizando Vue.js, GraphQL e Node !</h6>
        </div>
        <div id="main">
            <div class="container">
                <div class="row">
                    <div class="col-md">
                        <h5>Prefixos <span class="badge badge-info">{{ prefixes.length }}</span></h5>
                        <div class="card">
                            <div class="card-body">
                                <ul class="list-group">
                                    <li class="list-group-item" v-for="prefix in prefixes" v-bind:key="prefix">
                                        {{ prefix }}
                                    </li>
                                    <br>
                                    <input type="text" class="form-control" name="prefix">
                                </ul>
                            </div>
                        </div>
                    </div>
                    <div class="col-md">
                        <h5>Prefixos <span class="badge badge-info">{{ sufixes.length }}</span></h5>
                        <div class="card">
                            <div class="card-body">
                                <ul class="list-group">
                                    <li class="list-group-item" v-for="sufix in sufixes" v-bind:key="sufix">
                                        {{ sufix }}
                                    </li>
                                    <br>
                                    <input type="text" class="form-control" name="sufix">
                                </ul>
                            </div>
                        </div>
                    </div>
                </div>
                <br>
                <h5>Domínios <span class="badge badge-info">{{ domain.length }}</span></h5>
                <div class="card">
                    <div class="card-body">
                        <ul class="list-group">
                            <li class="list-group-item" v-for="domain in domains" v-bind:key="domain">
                                {{ domain }}
                            </li>
                        </ul>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import "bootstrap/dist/css/bootstrap.css"
import "font-awesome/css/font-awesome.css"

export default {
    name: 'app',
    data() {
        return {
            prefixes: ['Air', 'Jet', 'Flight'],
            sufixes: ['Hub', 'Mark', 'Station'],
            domains: ['AirHub', 'AirMark', 'AirStation', 'JetHub', 'JetMark', 'JetStation', 'FlightHub', 'FlightMark', 'FlightStation']
        }
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

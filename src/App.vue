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
                                        <div class="row">
                                            <div class="col-md">
                                                {{ prefix }}
                                            </div>
                                            <div class="col-md text-right">
                                                <button class="btn btn-sm btn-danger" v-on:click="deletePrefix(prefix)"><i class="fa fa-trash"></i></button>
                                            </div>
                                        </div>
                                    </li>
                                    <br>
                                    <div class="input-group">
                                        <input type="text" class="form-control" v-model="prefix" v-on:keyup.enter="addPrefix(prefix)" placeholder="Digite o prefixo">
                                        <div class="input-group-append">
                                            <button class="btn btn-info" v-on:click="addPrefix(prefix)"><i class="fa fa-plus"></i></button>
                                        </div>
                                    </div>
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
                                         <div class="row">
                                            <div class="col-md">
                                                {{ sufix }}
                                            </div>
                                            <div class="col-md text-right">
                                                <button class="btn btn-sm btn-danger" v-on:click="deleteSufix(sufix)"><i class="fa fa-trash"></i></button>
                                            </div>
                                        </div>
                                    </li>
                                    <br>
                                    <div class="input-group">
                                        <input type="text" class="form-control" v-model="sufix" v-on:keyup.enter="addSufix(sufix)" placeholder="Digite o sufixo">
                                        <div class="input-group-append">
                                            <button class="btn btn-info" v-on:click="addSufix(sufix)"><i class="fa fa-plus"></i></button>
                                        </div>
                                    </div>
                                </ul>
                            </div>
                        </div>
                    </div>
                </div>
                <br>
                <h5>Domínios <span class="badge badge-info">{{ domains.length }}</span></h5>
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
            prefix: "",
            sufix: "",
            prefixes: ['Air', 'Jet', 'Flight'],
            sufixes: ['Hub', 'Mark', 'Station'],
            domains: ['AirHub', 'AirMark', 'AirStation', 'JetHub', 'JetMark', 'JetStation', 'FlightHub', 'FlightMark', 'FlightStation']
        }
    },
    methods: {
        addPrefix(prefix) {
            this.prefixes.push(prefix);
            this.prefix = "";
            this.generateDomains();
        },
        deletePrefix(prefix) {
            this.prefixes.splice(this.prefixes.indexOf(prefix), 1);
            this.generateDomains();
        },
        addSufix(sufix) {
            this.sufixes.push(sufix);
            this.sufix = "";
            this.generateDomains();
        },
        deleteSufix(sufix) {
            this.sufixes.splice(this.sufixes.indexOf(sufix), 1);
            this.generateDomains();
        },
        generateDomains() {
            this.domains = [];
            for(const prefix of this.prefixes) {
                for(const sufix of this.sufixes) {
                    this.domains.push(prefix + sufix);
                }
            }
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

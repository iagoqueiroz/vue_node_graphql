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
                            <li class="list-group-item" v-for="domain in domains" v-bind:key="domain.name">
                                <div class="row">
                                    <div class="col-md">
                                        {{  domain.name }}
                                    </div>
                                    <div class="col-md text-right">
                                        <a v-bind:href="domain.checkout" target="_blank" class="btn btn-sm btn-success"><i class="fa fa-shopping-cart"></i></a>
                                    </div>
                                </div>
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
            sufixes: ['Hub', 'Mark', 'Station']
        }
    },
    methods: {
        addPrefix(prefix) {
            this.prefixes.push(prefix);
            this.prefix = "";
        },
        deletePrefix(prefix) {
            this.prefixes.splice(this.prefixes.indexOf(prefix), 1);
        },
        addSufix(sufix) {
            this.sufixes.push(sufix);
            this.sufix = "";
        },
        deleteSufix(sufix) {
            this.sufixes.splice(this.sufixes.indexOf(sufix), 1);
        }
    },
    computed: {
        domains() {
            const domains = [];
            for(const prefix of this.prefixes) {
                for(const sufix of this.sufixes) {
                    const name = prefix + sufix;
                    const url = name.toLowerCase();
                    domains.push({
                        name,
                        checkout: `https://checkout.hostgator.com.br/?a=add&sld=${url}&tld=.com.br`
                    });
                }
            }

            return domains;
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

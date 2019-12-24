<template>
    <div>
        <div id="main">
            <div class="container">
                <div class="row">
                    <div class="col-md">
                        <AppItemList title="Prefixos" :items="prefixes" v-on:addItem="addPrefix" v-on:deleteItem="deletePrefix"></AppItemList>
                    </div>
                    <div class="col-md">
                        <AppItemList title="Sufixos" :items="sufixes" v-on:addItem="addSufix" v-on:deleteItem="deleteSufix"></AppItemList>
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
import axios from 'axios';
import AppItemList from './AppItemList'

export default {
    name: 'DomainList',
    components: {
        AppItemList
    },
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
    },
    created() {
        axios({
            url: "http://localhost:4000",
            method: "post",
            data: {
                query: `
                    {
                        prefixes: items (type: "prefix") {
                            id
                            type
                            description
                        }
                        sufixes: items (type: "sufix") {
                            description
                        }
                    }
                `
            }
        }).then(resolve => {
            const query = resolve.data;
            this.prefixes = query.data.prefixes.map(prefix => prefix.description);
            this.sufixes = query.data.sufixes.map(sufix => sufix.description);
        });
    }
}
</script>

<style>

</style>
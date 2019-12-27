<template>
    <div>
        <div id="main">
            <div class="container">
                <div class="row">
                    <div class="col-md">
                        <AppItemList title="Prefixos" type="prefix" :items="items.prefix" v-on:addItem="addItem" v-on:deleteItem="deleteItem"></AppItemList>
                    </div>
                    <div class="col-md">
                        <AppItemList title="Sufixos" type="sufix" :items="items.sufix" v-on:addItem="addItem" v-on:deleteItem="deleteItem"></AppItemList>
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
            items: {
                sufix: [],
                prefix: []
            }
        }
    },
    methods: {
        addItem(item) {
            // this.prefixes.push(prefix);
            axios({
                url: "http://localhost:4000",
                method: "post",
                data: {
                    query: `
                        mutation ($item: ItemInput) {
                            newItem: saveItem(item: $item) {
                                id
                                type
                                description
                            }
                        }
                    `,
                    variables: {
                        item
                    }
                }
            }).then(resolve => {
                const query = resolve.data;
                const newItem = query.data.newItem;
                this.items[item.type].push(newItem);
            });
        },
        deleteItem(item) {
            axios({
                url: "http://localhost:4000",
                method: "post",
                data: {
                    query: `
                        mutation ($id: Int) {
                            deleted: deleteItem(id: $id)
                        }
                    `,
                    variables: {
                        id: item.id
                    }
                }
            }).then(() => {
                this.getItems(item.type);
            });
        },
        getItems(type) {
            axios({
                url: "http://localhost:4000",
                method: "post",
                data: {
                    query: `
                        query ($type: String) {
                            items (type: $type) {
                                id
                                type
                                description
                            }
                        }
                    `,
                    variables: {
                        type
                    }
                }
            }).then(resolve => {
                const query = resolve.data;
                this.items[type] = query.data.items;
            });
        },
    },
    computed: {
        domains() {
            const domains = [];
            for(const prefix of this.items.prefix) {
                for(const sufix of this.items.sufix) {
                    const name = prefix.description + sufix.description;
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
        this.getItems("prefix");
        this.getItems("sufix");
    }
}
</script>

<style>

</style>
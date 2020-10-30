<template>
    <div class="container">
        <h2>Filter</h2>

        <!--Search container -->
        <div class="row">
            <b-form class="form-inline">

                <input class="form-control" type="text" placeholder="" aria-label="Search" v-model="searchText">
                <b-button @click="searchModules" variant="outline-primary">
                    <b-icon icon="search"></b-icon>Search
                </b-button>

            </b-form>
        </div>

        <!--Checkbox buttons -->
        <br>
        <b-form-group label="Using options array:">
            <b-form-checkbox-group v-model="selected" :options="options" name="buttons-1" buttons
                button-variant="outline-secondary"></b-form-checkbox-group>
        </b-form-group>

        <!-- Generated/Filtered list -->

        <ul>
            <li v-for="item in filteredModules" :key="item.name">
                {{ item.name}}
            </li>
        </ul>
        <p> {{ this.selected }} </p>


        <!-- <div>
            <label for="range-1">Example range with min and max</label>
            <b-form-input id="range-1" v-model="minimumDifficulty" type="range" min="0" max="10"></b-form-input>
            <div class="mt-2">Value: {{ this.minimumDifficulty }}</div>
        </div>

        <div>
            <label for="range-1">Difficulty level</label>
            <b-form-input id="range-1" v-model="from" type="range" min="0" max="10"></b-form-input>
            <div class="mt-2">Value: {{ from }}</div>
        </div> -->


    </div>

</template>

<script>
    export default {
        data() {
            return {
                searchText: '',
                options: [{
                        text: 'DevOps',
                        value: 'Devops'
                    },
                    {
                        text: 'Security',
                        value: 'Security'
                    },
                    {
                        text: 'Programming',
                        value: 'Programming'
                    }
                ],
                selected: [],
                modules: [{
                        id: 1,
                        ownerId: 1,
                        version: 2,
                        name: "Cloud Providers",
                        categories: ["Devops"],
                        description: "An overview of the cloud providers avaliable",
                        difficulty: 1
                    },
                    {
                        id: 2,
                        ownerId: 1,
                        version: 1,
                        name: "Security Essentials",
                        categories: ["Security"],
                        description: "All the tools you need for security",
                        difficulty: 3
                    },
                    {
                        id: 3,
                        ownerId: 2,
                        version: 1,
                        name: "Java EE 8 APIs",
                        description: "An overview of the APIs avaliable within Java EE 8",
                        difficulty: 4,
                        categories: ["Programming"]
                    },
                    {
                        id: 4,
                        version: 1,
                        name: "Java - the basics",
                        summary: "Introduction to Java",
                        description: "A much longer description of the course",
                        ownerId: 1234,
                        categories: ["Programming"],
                        difficulty: 4
                    },
                    {
                        id: 5,
                        version: 1,
                        name: "Java2",
                        summary: "Advanced Java",
                        description: "A much longer description of the course",
                        ownerId: 1234,
                        categories: ["Programming", "Security", "Devops"],
                        difficulty: 10
                    },
                        {
                        id: 6,
                        version: 1,
                        name: "Java2",
                        summary: "Advanced Java",
                        description: "A much longer description of the course",
                        ownerId: 1234,
                        categories: ["Programming", "Security", "Devops"],
                        difficulty: 10
                    },
                        {
                        id: 5,
                        version: 1,
                        name: "Java2",
                        summary: "Advanced Java",
                        description: "A much longer description of the course",
                        ownerId: 1234,
                        categories: ["Programming", "Security", "Devops"],
                        difficulty: 10
                    },
                        {
                        id: 5,
                        version: 1,
                        name: "Java2",
                        summary: "Advanced Java",
                        description: "A much longer description of the course",
                        ownerId: 1234,
                        categories: ["Programming", "Security", "Devops"],
                        difficulty: 10
                    },
                        {
                        id: 5,
                        version: 1,
                        name: "Java2",
                        summary: "Advanced Java",
                        description: "A much longer description of the course",
                        ownerId: 1234,
                        categories: ["Programming", "Security", "Devops"],
                        difficulty: 10
                    },
                ],
            }
        },
        computed: {
            filteredModules: function () {
                return this.filterModulesByCategory(this.filterModulesBySearch(this.modules))
            }
            },

            methods: {
                filterModulesByCategory: function(modules) {
                    if (this.selected.length == 0) {
                        return modules;
                    } else {
                        let filteredModules = [];
                        modules.forEach(module => {
                            var count = 0;
                            module.categories.forEach(category => {
                                count = count + this.selected.filter((cat) => {
                                    return cat === category;
                                }).length

                            })
                            if (count === this.selected.length) {
                                filteredModules.push(module);
                            }
                        })
                        return filteredModules;
                    }
                },
                filterModulesBySearch: function(modules) {
                    let vm = this;
                    if (vm.searchText !== '') {
                        return modules.filter(item => {
                            var reg = new RegExp("\\b" + vm.searchText + "", "ig");
                            return reg.test(item.name);
                        })
                    } else {
                        return modules;
                    }
                }
            }
        }
    
</script>
<style>
    ul {
        list-style: none;
        text-align: left;
        padding-left: 0;
    }

    li {
        border-bottom: 0.01rem solid #D3D3D3;
    }
</style>
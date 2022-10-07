<script>
    export default {
        data() {
            return {
                label: "uk-button uk-label uk-label-success",
                tutorials: [
                    {
                        title: "JavaScript",
                        description: "Create a JavaScript code snippet that will be executed on your browser.",
                        status: "Pending"
                    },
                    {
                        title: "CSS",
                        description: "CSS is the language we use to style an HTML document. CSS describes how HTML elements should be displayed. ",
                        status: "Published"
                    },
                    {
                        title: "PHP",
                        description: "A popular general-purpose scripting language that is especially suited to web development. Fast, flexible and pragmatic.",
                        status: "Published"
                    }
                ]
            }
        },
        methods: {
            labelControl(val) {
                this.label = val == "Published" ? "uk-button uk-label uk-label-success" : "uk-button uk-label uk-label-warning";
                return this.label;
            },
            clearList() {
                this.tutorials = [];
            },
            changeStatus(index) {
                let list = this.tutorials;
                list[index].status = list[index].status == "Published" ? "Pending" : "Published";
                this.tutorials = list;
            }
        }
    }
</script>

<template>
    <div class="uk-width-1-2 uk-flex uk-flex-center uk-flex-column uk-margin-large-top">
        <ul uk-accordion="collapsible: false">
            <li v-for="(item, i) in tutorials" key="i">
                <a class="uk-accordion-title" href="#">{{item.title}}</a>
                <div class="uk-accordion-content">
                    <p>{{item.description}}</p>
                    <button :class="labelControl(item.status)" @click="changeStatus(i)">{{item.status}}</button>
                </div>
            </li>
        </ul>
        <button class="uk-button uk-button-danger uk-margin-auto" @click="clearList">Remove All</button>
    </div>
</template>

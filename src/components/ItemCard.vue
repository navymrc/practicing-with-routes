<script>
    export default {
        data() {
            return {
                label: "uk-button uk-label uk-label-success",
                tutorials: []
            }
        },
        methods: {
            storage() {
                localStorage.setItem('tutorials', JSON.stringify([]));
            },
            labelControl(val) {
                this.label = val == "Published" ? "uk-button uk-label uk-label-success" : "uk-button uk-label uk-label-warning";
                return this.label;
            },
            clearList() {
                this.storage();
                this.tutorials = [];
            },
            changeStatus(index) {
                let list = this.tutorials;
                let tutorials = JSON.parse(localStorage.getItem('tutorials'));
                if (tutorials == undefined) return this.storage();
                tutorials[index].status = tutorials[index].status == "Published" ? "Pending" : "Published";
                localStorage.setItem('tutorials', JSON.stringify(tutorials));
                list[index].status = list[index].status == "Published" ? "Pending" : "Published";
                this.tutorials = list;
            }
        },
        mounted() {
            let tutorials = JSON.parse(localStorage.getItem('tutorials'));
            if (tutorials == undefined) this.storage();
            this.tutorials = tutorials;
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

<script>
    export default {
        data() {
            return {
                form: {
                    title: "",
                    description: "",
                    status: "Pending"
                }
            };
        },
        methods: {
            storage() {
                localStorage.setItem('tutorials', JSON.stringify([]));
            },
            save(event) {
                event.preventDefault();
                function init(list) {
                    let titles = list.map(item => item.title);
                    if (!titles.includes(this.form.title)) {
                        list.push(this.form);
                        localStorage.setItem('tutorials', JSON.stringify(list));
                        UIkit.notification(`New Tutorial "${this.form.title}" Saved`, {pos: 'bottom-right', status:'success'});
                        this.form = {
                            title: "",
                            description: "",
                            status: "Pending"
                        };
                        return true;
                    }
                    UIkit.notification(`"${this.form.title}" already exist!!!`, {pos: 'bottom-right', status:'danger'});
                    return false;
                }
                let list = JSON.parse(localStorage.getItem('tutorials'));
                if (list == undefined) {
                    this.storage();
                    let binded = init.bind(this);
                    binded(list);
                }
                else {
                    let binded = init.bind(this);
                    binded(list);
                }
            }
        }
    }
</script>

<template>
    <div class="uk-flex uk-flex-center">
        <form class="uk-form-stacked uk-width-2-3@s" @submit="save">
            <div class="uk-margin">
                <label for="title" class="uk-form-label">Title</label>
                <div class="uk-form-controls">
                    <input v-model="form.title" type="text" class="uk-input" id="title">
                </div>
            </div>
    
            <div class="uk-margin">
                <label for="description" class="uk-form-label">Description</label>
                <div class="uk-form-controls">
                    <textarea v-model="form.description" id="description" class="uk-textarea" rows="5"></textarea>
                </div>
            </div>
            <div>
                <input type="submit" class="uk-button uk-button-primary" value="Save">
            </div>
        </form>
    </div>
</template>

<style>
    label {
        cursor: pointer;
    }
</style>

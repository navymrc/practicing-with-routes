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
        }
    }
</script>

<template>
    <div class="uk-flex uk-flex-center">
        <form class="uk-form-stacked uk-width-1-2">
            <div class="uk-margin">
                <label for="title" class="uk-form-label">Text</label>
                <div class="uk-form-controls">
                    <input v-model="form.title" type="text" class="uk-input" id="title">
                </div>
            </div>
    
            <div class="uk-margin">
                <label for="description" class="uk-form-label">Select</label>
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

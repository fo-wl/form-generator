<template>
<div id="app" class="h-screen w-screen flex items-center justify-center">
    <div class="w-1/2">
        <div v-for="field in schema.fields" class="border mb-3 p-3">
            <label v-if="field.label" :for="field.id" class="text-sm mb-2 text-gray-600">{{ field.label }} <span v-if="field.required" class="text-red-600">*</span></label>
            <field :id="field.id" :is="field.type" class="bg-white focus:outline-none focus:shadow-outline border border-gray-300 rounded-lg py-2 px-4 block leading-normal text-gray-600" :class="{'cursor-not-allowed bg-gray-300': field.disabled, 'w-full': field.inputType != 'checkbox' && field.inputType != 'radio'}" :placeholder="field.placeholder" @input="e => { field.model = (field.inputType == 'checkbox' || field.inputType == 'radio') ? e.target.checked : e.target.value; toggleLocalStorage(field.id, field.model) }" :value="getItem(field.id)" :disabled="field.disabled" :type="field.inputType" :maxlength="field.maxlength" :max="field.max" :min="field.min">
                <option v-if="field.type == 'select'" selected disabled>{{ field.placeholder }}</option>
                <option v-if="field.type == 'select'" v-for="option in field.options" @change="e => { field.model = e.target.value; toggleLocalStorage(field.id, field.model) }" :selected="option == getItem(field.id)">{{ option }}</option>
            </field>
            <span v-if="field.hint" class="text-gray-500 text-xs">{{ field.hint }}</span>
        </div>

        <div v-if="schema.fields.length == 0" class="border mb-3 p-3 text-red-600 text-center">Empty fields schema</div>

        <div v-if="errors.length > 0" class="mb-3 border p-2 text-red-700 text-sm">
            <ul class="list-disc list-inside">
                <li v-for="error in errors">{{ error }}</li>
            </ul>
        </div>

        <button class="w-full bg-transparent hover:bg-blue-500 text-blue-700 font-semibold hover:text-white py-2 px-4 border border-blue-500 hover:border-transparent rounded" @click="validate">Validate</button>
    </div>
</div>
</template>

<script>
export default {
    name: 'app',
    data() {
        return {
            schema: {
                fields: []
            },
            errors: []
        }
    },
    methods: {
        toggleLocalStorage: function (id, model) {
            (model.length > 0 || model == true) ? localStorage.setItem(id, model): localStorage.removeItem(id)
        },
        getItem: function (id) {
            return localStorage.getItem(id)
        },
        validate: function () {
            this.errors = []
            for (let field in this.schema.fields) {
                field = this.schema.fields[field]

                if (field.required && (!field.model || field.model.length == 0))
                    this.errors.push("Field " + field.id + " required!")

                if (field.max && (!field.model || field.model.length > field.max))
                    this.errors.push("Field max " + field.max + "!")

                if (field.min && (!field.model || field.model.length < field.min))
                    this.errors.push("Field min " + field.min + "!")

                if (field.maxlength && (!field.model || field.model.length > field.maxlength))
                    this.errors.push("Field maxlength " + field.maxlength + "!")
            }
        }
    }
}
</script>

<style></style>

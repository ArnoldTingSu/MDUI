<script setup lang="ts">
import {ref} from "vue"

const emit = defineEmits(["submit"])
const props = defineProps<{
    //general object setting, should confine this to a post-request
    post: Record<string, any>;
}>();
const form = ref({
    title: "",
    tags: [],
    published: null,
    body: "",
    image: [],
    ...props.post,
});


//form validation logic
const valid = ref(true);

function isNotEmpty(value: string[]) {
    if (value && value.length) return true;
    return "Please choose atleast one option";
}

function isRequired(value: string) {
    if (value) return true;
    return "Field is required";
}

async function asyncValidation(value: string) {
    const res = await fetch(`https://httpbin.org/status/${value}`);
    if (res.ok) return true;
    return "Bad response code";
}

function handleSubmit() {
    if(!valid.value) return;
    console.log("submitting", form.value);
    emit("submit");
}

const submitBtn = ref();
const submit = () => submitBtn.value.click();

defineExpose({ submit });

</script>

<template>
<v-form v-model="valid" @submit.prevent="handleSubmit" ref="formE1">
    <v-row>
        <v-col cols="3">
            <v-switch label="Published" v-model="form.published"></v-switch>
        </v-col>
        <v-col cols="3">
            <v-checkbox
                indeterminate
                v-model="form.published"
                label="Published"
            >
            </v-checkbox>
        </v-col>
    </v-row>
    <v-text-field 
        v-model="form.title" 
        label="Title"
        :rules="[asyncValidation]"
    />
    <v-combobox
        v-model="form.tags"
        :items="['News', 'Tutorials', 'Event']"
        label="Tags"
        :rules="[isNotEmpty]"
        multiple
        chips
    >
    </v-combobox>
    <v-file-input
        accept="image/png, image/jpeg, image/bmp"
        placeholder="Upload a featured image"
        prepend-icon="mdi-camera"
        label="Featured Image"
        v-model="form.image"
    >
    </v-file-input>
    <v-textarea label="Post Body" v-model="form.body"></v-textarea>
    Form is Valid? {{ valid }}
    <button ref="submitBtn" type="submit" class="d-none">Submit</button>
</v-form>
</template>
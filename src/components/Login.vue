<template>
    <div>
        <b-form @submit="onSubmit" @reset="onReset" v-if="show">
            <b-form-group
                    id="input-group-1"
                    label="Email address:"
                    label-for="input-1"
                    description="We'll never share your email with anyone else."
            >
                <b-form-input
                        id="input-1"
                        v-model="form.email"
                        type="email"
                        required
                        placeholder="Enter email"
                ></b-form-input>
            </b-form-group>

            <b-form-group id="input-group-2" label="Your Password:" label-for="input-2">
                <b-form-input
                        id="input-2"
                        v-model="form.pass"
                        required
                        placeholder="Enter password"
                ></b-form-input>
            </b-form-group>
            <b-button type="submit" variant="primary">Submit</b-button>
            <b-button type="reset" variant="danger">Reset</b-button>
        </b-form>
    </div>
</template>

<script>
    import {BForm, BFormGroup, BFormInput, BButton} from 'bootstrap-vue'

    export default {
        name: 'Login',
        components:{
          'b-form': BForm,
          'b-form-group': BFormGroup,
            'b-form-input': BFormInput,
            'b-button': BButton,
        },
        data() {
            return {
                form: {
                    email: '',
                    pass: '',
                },
                show: true
            }
        },
        methods: {
            onSubmit(evt) {
                evt.preventDefault();
                const parsed = JSON.stringify(this.form);
                localStorage.setItem('user', parsed);
                location.reload();
            },
            onReset(evt) {
                evt.preventDefault();
                // Reset our form values
                this.form.email = '';
                this.form.pass = '';
                // Trick to reset/clear native browser form validation state
                this.show = false;
                this.$nextTick(() => {
                    this.show = true
                })
            }
        }
    }
</script>

<style scoped>

</style>
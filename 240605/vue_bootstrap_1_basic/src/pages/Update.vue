<template>
    <div class="container">
        <div class="px-5">
            <h1 class="mb-3">update</h1>
            <form class="needs-validation" novalidate @submit.prevent="submit">
                <div class="row g-3">
                    <div class="col-sm-6">
                        <label for="firstName" class="form-label">First name</label>
                        <input v-model="firstName" type="text" class="form-control" id="firstName" placeholder="" value="" required>
                        <div :class="firstName ? 'invalid-feedback':''">
                            Valid first name is required.
                        </div>
                    </div>

                    <div class="col-sm-6">
                        <label for="lastName" class="form-label">Last name</label>
                        <input v-model="lastName" type="text" class="form-control" id="lastName" placeholder="" value="" required>
                        <div :class="lastName ? 'invalid-feedback':''">
                            Valid last name is required.
                        </div>
                    </div>

                    <div class="col-12">
                        <label for="email" class="form-label">Email <span
                                class="text-body-secondary"></span></label>
                        <input v-model="email" @change="changeEmail" type="email" class="form-control" id="email" placeholder="you@example.com">
                        <div :class="email_class">
                            Please enter a valid email address for shipping updates.
                        </div>
                    </div>

                    <div class="col-md-12">
                        <label for="gender" class="form-label">Gender</label>
                        <select v-model="gender" class="form-select" id="gender" required>
                            <option value="">Choose...</option>
                            <option>Male</option>
                            <option>Female</option>
                        </select>
                        <div :class="gender ? 'invalid-feedback' : ''">
                            Please select a valid gender.
                        </div>
                    </div>
                    <div class="col-sm-6">
                      <button class="btn btn-primary btn-lg w-100" type="submit">Submit!</button>
                    </div>
                    <div class="col-sm-6">
                      <button class="btn btn-primary btn-lg w-100" type="reset">Clear</button>
                    </div>
                </div>
            </form>
        </div>

    </div>
</template>
<script setup>
import { ref } from 'vue';
import json from '@/MOCK_DATA.json';
const member = json[0];

const firstName = ref(member.first_name);
const lastName = ref(member.last_name);
const email = ref(member.email);
const gender = ref(member.gender);
const email_class = ref('invalid-feedback');


const changeEmail = (e) => {
    let regex = /^[a-zA-Z0-9+-\_.]+@[a-zA-Z0-9-]+\.[a-zA-Z0-9-.]+$/;
    if(email.value && regex.test(email.value) == false){
        email_class.value = '';
    }else{
        email_class.value = 'invalid-feedback';
    }
}

const submit = (e) => {
    //전통적으로 form에서 input 값 가져오는 방법
    //formName.inputName
    let member = {
        firstName: firstName.value,
        lastName: lastName.value,
        email: email.value,
        gender: gender.value,
    }
    alert('member : ' + JSON.stringify(member));
}

</script>
<template>
    <div class="container mt-5">
        <div class="card">
            <div class="card-header">
                <h4>Add Students</h4>
            </div>
            <div class="card-body">
                <ul class="alert alert-warning" v-if="Object.keys(this.errorList).length > 0">
                    <li class="mb-0 ms-3" v-for="(error, index) in this.errorList" :key="index">
                        {{ error }}
                    </li>
                </ul>
                <div class="form-group mb-3">
                    <label for="name" class="form-label">Name</label>
                    <input type="text" v-model="model.student.name" name="name" id="name" class="form-control">
                </div>
                <div class="form-group mb-3">
                    <label for="course" class="form-label">Course</label>
                    <input type="text" v-model="model.student.course" name="course" id="course" class="form-control">
                </div>
                <div class="form-group mb-3">
                    <label for="email" class="form-label">Email</label>
                    <input type="email" v-model="model.student.email" name="email" id="email" class="form-control">
                </div>
                <div class="form-group mb-3">
                    <label for="phone" class="form-label">Phone</label>
                    <input type="text" v-model="model.student.phone" name="phone" id="phone" class="form-control">
                </div>
                <div class="form-group mb-3">
                    <button type="submit" @click="saveStudent" class="btn btn-primary">Submit</button>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import axios from 'axios'

export default {
    name: 'studentCreate',
    data() {
        return {
            errorList: '',
            model: {
                student: {
                    name: '',
                    course: '',
                    email: '',
                    phone: ''
                }
            }
        }
    },
    methods: {
        saveStudent() {
            var myThis = this
            axios.post('http://localhost:3000/students', this.model.student)
                .then(res => {
                    console.log(res.data);

                    this.model.student = {
                        name: '',
                        course: '',
                        email: '',
                        phone: ''
                    }
                })
                .catch(function (error) {
                    if (error.response) {
                        if (error.response.status == 400) {
                            myThis.errorList = error.response.data.message
                        }
                        console.log(error.response);
                    } else if (error.request) {
                        console.log(error.request);
                    } else {
                        console.log('Error', error.message);
                    }
                })
        }
    }
}
</script>
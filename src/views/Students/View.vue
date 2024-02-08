<template>
    <div>
        <div class="card">
            <div class="card-header">
                <h4>Students <RouterLink to="students/create" class="btn btn-primary float-end">Add Student</RouterLink>
                </h4>
            </div>
            <div class="card-body">
                <table class="table table-bordered">
                    <thead>
                        <tr>
                            <th>ID</th>
                            <th>Name</th>
                            <th>Course</th>
                            <th>Email</th>
                            <th>Phone</th>
                            <th>Action</th>
                        </tr>
                    </thead>
                    <tbody>
                        <tr v-for="(student, index) in this.students" :key="index">
                            <td>{{ index + 1 }}</td>
                            <td>{{ student.name }}</td>
                            <td>{{ student.course }}</td>
                            <td>{{ student.email }}</td>
                            <td>{{ student.phone }}</td>
                            <td>
                                <RouterLink :to="{ path: '/students/' + student.id_student + '/edit' }"
                                    class="btn btn-success">Edit</RouterLink>
                                <button type="button" @click="deleteStudent(student.id_student)"
                                    class="btn btn-danger">Delete</button>
                            </td>
                        </tr>
                    </tbody>
                </table>
            </div>
        </div>
    </div>
</template>

<script>
import axios from 'axios'

export default {
    name: 'students',
    data() {
        return {
            students: []
        }
    },
    mounted() {
        this.getStudents();
    },
    methods: {
        getStudents() {
            axios.get('http://localhost:3000/students').then(res => {
                this.students = res.data
                console.log(res.data);
            });
        },
        deleteStudent(id) {
            if (confirm('Are you sure, you want to delete this data?')) {
                axios.delete(`http://localhost:3000/students/${id}`)
                    .then(res => {
                        // this.students = res.data
                        // alert(res.data.message)
                        this.getStudents()
                    });
            }
        }
    }
}
</script>
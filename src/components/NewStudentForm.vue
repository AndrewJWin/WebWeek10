<template>
    <div>
        <div class="alert alert-danger" v-show="errors.length > 0">
            <li v-for="error in errors" v-bind:key="error">{{error}}</li>
        </div>


        <div class="card add-student m-2 p-2">
            <h4 class="card-title">Add new student</h4>

            <div class="form-group">
                <label for="name">Name</label>
                <input id="name" class="form-control" v-model.trim="newStudentName">
            </div>
            <div class="form-group">
                <label for="starID">Star ID</label>
                <input id="starID" class="form-control" v-model.trim="newStarID">
            </div>
            <button class="btn btn-primary" v-on:click="addStudent">Add</button>
        </div>
    </div>
</template>

<script>
export default {
    name: "NewStudentForm",
    emits: ["student-added"],
    data() {
                return {
                    newStudentName: "",
                    newStarID: "",
                    students: [
                        { name: "TestStudent1", starID: "ab1234cd", present:false},
                        { name: "TestStudent2", starID: "ef5678gh", present:false}
                    ],
                    errors: [],
                    mostRecentStudent: {}
                }
            },
            methods: {
                addStudent() {
                    this.errors = [];
                    
                    if (!this.newStudentName) this.errors.push("Student name must be entered.");
                    if (!this.newStarID) this.errors.push("StarID must be entered.");
                    if (this.students.find(s => s.starID == this.newStarID)) this.errors.push("Student is already in the list!");

                    if (this.errors.length == 0) {
                        let student = { name: this.newStudentName, starID: this.newStarID, present:false }
                        this.$emit("student-added", student);
                        this.newStarID = "";
                        this.newStudentName = "";
                    }
                },
                arrivedOrLeft(student) {
                    this.mostRecentStudent = student;
                }
            }
}
</script>

<style>

</style>
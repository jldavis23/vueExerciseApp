<script>
export default {
    data() {
        return {
            chosenExercise: null,
            input1: null,
            input2: null,
            input3: null,
            inputDate: null,
            exerciseList: []
        }

    },
    methods: {
        addExercise() {
            if (this.chosenExercise === 'timeDistance') {
                this.exerciseList = [...this.exerciseList, { type: this.chosenExercise, time: this.input1, distance: this.input2, date: this.inputDate }]
            } else if (this.chosenExercise === 'number') {
                this.exerciseList = [...this.exerciseList, { type: this.chosenExercise, quantity: this.input1, date: this.inputDate }]
            } else if (this.chosenExercise === 'setRepWeight') {
                this.exerciseList = [...this.exerciseList, { type: this.chosenExercise, sets: this.input1, reps: this.input2, weight: this.input3, date: this.inputDate }]
            }
            this.chosenExercise = null,
                this.input1 = null,
                this.input2 = null,
                this.input3 = null,
                this.inputDate = null,
                console.log(this.exerciseList)
        }
    }
}
</script>

<template>
    <div class="page-wrapper">
        <h1>ExerciseTrack</h1>

        <form @submit.prevent="addExercise">
            <h2>Add An Exercise</h2>
            <div class="input-group">
                <label>Choose an exercise</label>
                <select required v-model="chosenExercise">
                    <option disabled value="">Please select one</option>
                    <option value="Running">Running</option>
                    <option value="Cycling">Cycling</option>
                    <option value="Squats">Squats</option>
                    <option value="Push-ups">Push-ups</option>
                    <option value="Bench Press">Bench Press</option>
                    <option value="Deadlift">Deadlift</option>
                </select>
            </div>

            <div class="input-group" v-if="chosenExercise">
                <label v-if="chosenExercise === 'timeDistance'">Time</label>
                <label v-if="chosenExercise === 'number'">Quantity</label>
                <label v-if="chosenExercise === 'setRepWeight'">Sets</label>
                <input type="text" v-model="input1" required>
            </div>

            <div class="input-group" v-if="chosenExercise === 'timeDistance' || chosenExercise === 'setRepWeight'">
                <label v-if="chosenExercise === 'timeDistance'">Disance</label>
                <label v-if="chosenExercise === 'setRepWeight'">Reps</label>
                <input type="text" v-model="input2" required>
            </div>

            <div class="input-group" v-if="chosenExercise === 'setRepWeight'">
                <label>Weight</label>
                <input type="text" v-model="input3" required>
            </div>

            <div class="input-group" v-if="chosenExercise">
                <label>Date</label>
                <input type="date" v-model="inputDate" required>
            </div>


            <button type="submit">ADD EXERCISE</button>
        </form>

        <div>
            <h2>Your Exercises</h2>
            <div v-for="exercise in exerciseList" class="exercise">
                {{ exercise.type }}
            </div>
        </div>
        
    </div>
</template>

<style scoped>
.page-wrapper {
    margin: auto;
    max-width: 750px;
    
}

h1 {
    text-align: center;
    font-size: 40px;
    color: #474d32
}

form {
    margin-bottom: 80px;
}

.input-group {
    margin: 20px 0;
}

select,
input {
    display: block;
    border: 1px solid rgb(197, 197, 197);
    padding: 10px;
    border-radius: 3px;
    width: 100%;
}

label {
    display: block;
    margin-bottom: 5px;
}

button {
    display: block;
    border: none;
    padding: 10px;
    border-radius: 3px;
    background-color: #474d32;
    color: #fff;
    cursor: pointer;
}

.exercise {
    background-color: white;
    padding: 15px;
    margin: 10px 0;
}
</style>

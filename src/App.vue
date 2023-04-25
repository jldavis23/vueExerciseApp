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
            if (this.chosenExercise === 'Running' || this.chosenExercise === 'Cycling') {
                this.exerciseList = [...this.exerciseList, { type: this.chosenExercise, stats: [{ label: 'time', value: this.input1 }, { label: 'distance', value: this.input2 }], date: this.inputDate }]
            } else if (this.chosenExercise === 'Squats' || this.chosenExercise === 'Push-ups') {
                this.exerciseList = [...this.exerciseList, { type: this.chosenExercise, stats: [{label: 'quantity', value: this.input1}], date: this.inputDate }]
            } else if (this.chosenExercise === 'Bench Press' || this.chosenExercise === 'Deadlift') {
                this.exerciseList = [...this.exerciseList, { type: this.chosenExercise, stats: [{label: 'sets', value: this.input1}, {label: 'reps', value: this.input2}, {label: 'weight', value: this.input3}], date: this.inputDate }]
            }
            this.chosenExercise = null
            this.input1 = null
            this.input2 = null
            this.input3 = null
            this.inputDate = null
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
                <label>{{ chosenExercise === 'Running' || chosenExercise === 'Cycling' ? 'Time' : chosenExercise ===
                    'Squats' || chosenExercise === 'Push-ups' ? 'Quantity' : 'Sets' }}</label>
                <input type="text" v-model="input1" required>
            </div>

            <div class="input-group" v-if="chosenExercise && chosenExercise !== 'Squats' && chosenExercise !== 'Push-ups'">
                <label>{{ chosenExercise === 'Running' || chosenExercise === 'Cycling' ? 'Distance' : 'Reps' }}</label>
                <input type="text" v-model="input2" required>
            </div>

            <div class="input-group" v-if="chosenExercise === 'Bench Press' || chosenExercise === 'Deadlift'">
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
                <div>
                    <p class="smLabel">type</p>
                    <p>{{ exercise.type }}</p>
                </div>

                <div>
                    <p class="smLabel">date</p>
                    <p>{{ exercise.date }}</p>
                </div>

                <div class="stats">
                    <div v-for="stat in exercise.stats">
                        <p class="smLabel">{{ stat.label }}</p>
                        <p>{{ stat.value }}</p>
                    </div>
                </div>
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
    display: flex;
    justify-content: space-between;
}

.stats {
    display: flex;
    gap: 20px;
}

.stats p {
    text-align: center;
}

.smLabel {
    font-size: 12px;
    color: grey;
}
</style>

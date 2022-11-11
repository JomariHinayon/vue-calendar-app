<template>
    <div class="flex flex-row w-screen justify-center items-center">
        <div class="flex flex-col w-1/2 mt-5 text-center">
            <!-- Months -->
            <div class="pt-5 pb-2 flex flex-row justify-center">
                <button @click="minusMonth()">
                    <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="w-6 h-6">
                        <path stroke-linecap="round" stroke-linejoin="round" d="M15.75 19.5L8.25 12l7.5-7.5" />
                    </svg>
                </button>
                <p class="text-xl font-semibold px-5">{{ currentMonth }}</p>
                <button @click="addMonth()">
                    <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="w-6 h-6">
                        <path stroke-linecap="round" stroke-linejoin="round" d="M8.25 4.5l7.5 7.5-7.5 7.5" />
                    </svg>
                </button>
            </div>
            <!-- Year -->
            <div class="pb-3">
                <p class="font-semibold">{{ currentYear }}</p>
            </div>
            <!-- Weekdays -->
            <div class="flex flex-row">
                <p 
                 v-for="weekday in weekdays" 
                 :key="weekday"
                 class="w-10 mx-6"
                >
                    {{ weekday }}
                </p>
            </div>
            <!-- Days -->
            <div class="flex flex-row flex-wrap mt-3 ">
                <p
                 v-for="day in 31"
                 :key="day"
                 class="w-[5.5rem] mt-2"
                >
                 {{ day }}
                </p>
            </div>
        </div>
    </div>
</template>

<script>

    export default {
        name: 'Calendar',
        data() {
            return {
                weekdays: ['Mon', 'Tue', 'Wed', 'Thur', 'Fri', 'Sat', 'Sun'],
                monthNames: ['January', 'February', 'March', 'April', 'May', 'June', 'July', 'August', 'September', 'October', 'November', 'December'],
                monthIndex: new Date().getMonth(),
                currentMonth: new Date().toLocaleString('default', {month: "long"}),
                currentYear: new Date().getFullYear(),

            }
        },
        methods: {
            minusMonth() {
                if(this.monthIndex > 0) {
                    this.currentMonth = this.monthNames[this.monthIndex -= 1];
                }else {
                    this.monthIndex = this.monthNames.length - 1;
                    this.currentMonth = this.monthNames[this.monthIndex];
                    this.currentYear = Number(this.currentYear) - 1;
                }
            },
            addMonth() {
                if(this.monthIndex < this.monthNames.length - 1) {
                    this.currentMonth = this.monthNames[this.monthIndex += 1];   
                }else {
                    this.monthIndex = 0;
                    this.currentMonth = this.monthNames[this.monthIndex];
                    this.currentYear = Number(this.currentYear) + 1;
                }
            }
        }
    }
</script>

<style scoped>

</style>
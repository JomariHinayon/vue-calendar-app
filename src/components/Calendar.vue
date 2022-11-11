<template>
    <div class="flex flex-row w-screen justify-center items-center ">
        <div class="flex flex-col w-[45%] mt-5 text-center ">
            <!-- Months -->
            {{ currentDate() }}
            <div class="pt-5 pb-2 flex flex-row justify-center">
                <button @click="decreaseMonth()">
                    <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="w-6 h-6">
                        <path stroke-linecap="round" stroke-linejoin="round" d="M15.75 19.5L8.25 12l7.5-7.5" />
                    </svg>
                </button>
                <p class="text-xl font-semibold px-5">{{ currentMonthName }}</p>
                <button @click="increaseMonth()">
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
                 v-for="day in weekDayStart()"
                 :key="day"
                 class="w-[5.5rem] mt-2"
                >
                </p>
                <p
                 v-for="day in daysInMonth()"
                 :key="day"
                 class="w-[5.5rem] mt-2"
                 :class=" currentDate(day) ? 'bg-red-500 rounded-full text-white' : ''"
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
                weekdays: ['Sun','Mon', 'Tue', 'Wed', 'Thur', 'Fri', 'Sat'],
                months : ["January", "February", "March", "April", "May", "June", "July", "August", "September", "October", "November", "December"],
                currentMonth: new Date().getMonth(),
                currentMonthName: new Date().toLocaleString('default', {month: "long"}),
                currentYear: new Date().getFullYear(),
            }
        },
        methods: {
            daysInMonth() {
                return new Date(this.currentYear, this.currentMonth + 1, 0).getDate();
            },
            weekDayStart(){
                return new Date(this.currentYear, this.currentMonth + 1, 0).getDay(); 
            },
            decreaseMonth() {
                if(this.currentMonth > 0) {
                    this.currentMonthName = this.months[this.currentMonth -= 1];
                }else {
                    this.currentMonth = this.months.length - 1;
                    this.currentMonthName = this.months[this.currentMonth];
                    this.currentYear -= 1;
                }
            },
            increaseMonth() {
                if(this.currentMonth < this.months.length - 1) {
                    this.currentMonthName = this.months[this.currentMonth += 1];
                }else {
                    this.currentMonth = 0;
                    this.currentMonthName = this.months[this.currentMonth];
                    this.currentYear += 1;
                }
            },
            currentDate(day) {
                const currentDate = new Date().toDateString();
                const viewDate = new Date(this.currentYear, this.currentMonth, day).toDateString();
                return currentDate == viewDate;
            }
        }
    }
</script>

<style scoped>

</style>
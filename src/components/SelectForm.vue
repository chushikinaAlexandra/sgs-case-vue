<template>
    <select @change="changeSelectTown">
        <option disabled selected>Город</option>
        <option v-for="(town, index) in towns" :key="index" :value="index">{{ town }}</option>
    </select>
        <select @change="changeSelectDep">
            <option disabled selected>Цех</option>
            <template v-if="selectTown!==null">
                <option v-for="(d, index) in selectedDep.dep" :key="index" :value="d">{{ d }}</option>
            </template>
            <template v-else v-for="department in departments">
                <option v-for="(d, index) in department.dep" :key="index" :value="d">{{ d }}</option>
            </template>
        </select>
        <Select 
            @func="changeSelectStaff" 
            :selectDep="selectDep"
            :selectedStaff="selectedStaff"
            :staff="staff">Сотрудник
        </Select>
        
        <select @change="changeSelectTeam" >
            <option disabled selected>Бригада</option>
            <option value="1">1</option>
            <option value="2">2</option>
        </select>
        <select @change="changeSelectTime">
            <option disabled selected>Смена</option>
            <option value="8:00-20:00">8:00-20:00</option>
            <option value="20:00-8:00">20:00-8:00</option>
        </select>
        <Button @func="saveIntoCookie">Сохранить в Cookies</Button>
        <Button @func="watchInfo">Посмотреть cookies</Button>
        <div v-if="cookies">{{ cookies }}</div>
        

</template>
<script>
import Button from '@/components/Button.vue'
import Select from '@/components/Select.vue'

export default {
    components: {
        Button,
        Select
    },
    data() {
        return {
            selectTown: null,
            selectDep: '',
            selectTeam: '',
            selectStaff: '',
            cookies: null,
            obj: {},
            towns: [
            'Москва', 'Санкт-Петербург',
            'Екатеринбург', 'Пенза',
            'Брянск', 'Тамбов', 'Орел'
            ],

            selectedDep: null,
            selectedStaff: null,

            departments: [
                {idTown: 0, dep: ['001', '002']},
                {idTown: 1, dep: ['355', '572']},
                {idTown: 2, dep: ['477', '573']},
                {idTown: 3, dep: ['493', '856']},
                {idTown: 4, dep: ['033', '282']},
                {idTown: 5, dep: ['087']},
                {idTown: 6, dep: ['363']},
            ],
            staff: [
                {dep:'001', staff:['Петров', 'Сидоров', 'Козлов']},
                {dep:'002', staff:['Иванов', 'Колганова', 'Вьюгин']},
                {dep:'355', staff:['Белов', 'Рябов']},
                {dep:'572', staff:['Козлова', 'Никитин', 'Алексеев']},
                {dep:'477', staff:['Алексеева', 'Щербаков', 'Кисленко']},
                {dep:'573', staff:['Минина', 'Петрова', 'Иванова']},
                {dep:'493', staff:['Васильев', 'Бауков']},
                {dep:'856', staff:['Минин', 'Берюкова', 'Белянин']},
                {dep:'033', staff:['Миронова', 'Панина', 'Безруков']},
                {dep:'282', staff:['Прохоров', 'Калинин']},
                {dep:'087', staff:['Дедышева', 'Учуватов', 'Майоров']},
                {dep:'363', staff:['Щербаков', 'Кострова', 'Баранова']},
            ],
        }
    },
    methods: {
        changeSelectTown(event){
            this.selectTown=event.target.value
            this.selectedDep = this.departments[this.selectTown]
            this.obj.town = this.towns[this.selectTown]
        },
        changeSelectDep(event){
            this.selectDep=event.target.value
            let select = this.staff.find(el => el.dep == this.selectDep)
            this.selectedStaff = select.staff
            this.obj.department = this.selectDep
        },
        changeSelectStaff(event){
            this.obj.staff = event
        },
        changeSelectTeam(event){
            this.obj.team=event.target.value
        },
        changeSelectTime(event){
            this.obj.time=event.target.value
        },
        saveIntoCookie(){
        let objectString = JSON.stringify(this.obj);
        document.cookie = "myobject=" + objectString + "; expires="+ (new Date()).toDateString();
        },
        watchInfo(){
            this.cookies = document.cookie;
        }
    }
}

</script>
<style>
    .btn{
        margin-top: 10px;
    }
</style>
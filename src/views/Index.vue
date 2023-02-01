<template>
	<div>
		<Input placeholder="placeholder" size="lg" label="Введите название канала" @keyup.enter="getChanels">
			<template #helper>
				Тут могло бы быть описание поля ввода
			</template>
			<template #prefix>
				<svg aria-hidden="true" class="w-5 h-5 text-gray-500 dark:text-gray-400" fill="none" stroke="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg"> <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" 	d="M21 21l-6-6m2-5a7 7 0 11-14 0 7 7 0 0114 0z"></path></svg>
			</template>
			<template #suffix>
				<Button gradient="green-blue" @click="getChanels" outline>Поиск</Button>
			</template>
		</Input>
		<transition name="slide-fade" mode="out-in" class="mt-5">
			<div v-if="false ">
				<div class="flex gap-4 mt-5">
					<Button gradient="green-blue" @click="getChanels" outline>Отправить форму</Button>
					<Button gradient="red" @click="warningForm">неудачная отправка</Button>
				</div>
			</div>

			<div v-else-if="step === 1">
				<div class="grid gap-4 grid-cols-2 sm:grid-cols-3 md:grid-cols-4 lg:grid-cols-5 my-6" >
					<div v-for="n in 10" :key="n" class="flex flex-col gap-4 cursor-pointer"
						@click="selectedСhannel = n"
						:class="{ 'outline-green-500 outline-1 outline-double outline-offset-4': selectedСhannel == n }">
						<img src="@/assets/img/plug.jpg" alt="" class="aspect-video object-cover">
						<p>Название канала</p>
					</div>
				</div>
				<div class="flex flex-col gap-4">
					<Input placeholder="placeholder" label="Введите правило мониторинга" class="md:max-w-xs " />
					<Input placeholder="placeholder" label="Введите ваш username" class="md:max-w-xs" />
					<Button gradient="green-blue" @click="getUsers" outline class=" self-center md:self-start">Отправить форму</Button>
				</div>
			</div>
			<div v-else-if="step === 2">
				<list-group>
  				  	<list-group-item v-for="n in 10" class="cursor-pointer hover:text-green-500" @click="selectedUser = n" :class="{'text-green-500':selectedUser == n}" :hover="true">Пользователь №{{ n }}</list-group-item>
  				</list-group>				
				<Button gradient="green-blue" @click="sendUser" outline class=" self-center md:self-start mt-5">Отправить форму</Button>
			</div>
			<div v-else-if="step === 3">
				<Input placeholder="placeholder"  label="Введите код из телеграм" @keyup.enter="getChanels" />	
				<Button gradient="green-blue" @click="sendCode" outline class=" self-center md:self-start mt-5" >Отправить форму</Button>
			</div>

		</transition>
		<transition name="slideTop">
			<Alert :type="alert.type" :title="alert.title" class="mb-2 fixed top-0 left-0 w-full" v-if="isShowAlert">
			{{ alert.message }}</Alert>
		</transition>
	</div>
</template>

<script setup>
import { ref } from '@vue/reactivity'
import { watch } from '@vue/runtime-core'
import { Input, Button, Alert, ListGroup, ListGroupItem } from 'flowbite-vue'

let step = ref(0);

/* Блок функционала Alert */
let isShowAlert = ref(false),
	alert = ref({ title: null, message: null, type: null, duration: 5000, autoClose: true, })
watch(isShowAlert, (newValue, oldValue) => {
	if (alert.value.autoClose) {
		setTimeout(() => {
			isShowAlert.value = false
		}, alert.value.duration)
	}
})

const warningForm = () => {
	isShowAlert.value = true;
	alert.value.title = "Ошибка!"
	alert.value.type = "warning"
	alert.value.message = "При отправке формы произошла ошибка"
}

/* блок каналов */ 

const getChanels = () => {
	step.value = 1;
}

let selectedСhannel = ref(1)

/* блок рользователей */ 
let selectedUser = ref(null)

const getUsers = () => {
	step.value = 2;
}

/* блок с кодом */ 

const sendUser = () => {
	step.value = 3;
}

const sendCode = () => {
	step.value = 3;
}




</script>

<style>
.slideTop-enter-active {
	transition: all 0.5s ease-out;
}

.slideTop-leave-active {
	transition: all 0.5s ease-in;
}

.slideTop-enter-from,
.slideTop-leave-to {
	transform: translateY(-100%);
}

.slide-fade-enter-active {
	transition: all 0.3s ease-out;
}

.slide-fade-leave-active {
	transition: all 0.8s cubic-bezier(1, 0.5, 0.8, 1);
}

.slide-fade-enter-from,
.slide-fade-leave-to {
	transform: translateX(50%);
	opacity: 0;
}
</style>


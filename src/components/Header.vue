<template>
    <header class="Prose bg-slate-300 mb-5">
        <Navbar class="bg-transparent">
            <template #logo>
               Лого
            </template>
            <template #default="{ isShowMenu }">
                <NavbarCollapse :isShowMenu="isShowMenu">
                    <NavbarLink link="#">ссылка 1</NavbarLink>
                    <NavbarLink link="#">ссылка 2</NavbarLink>
                    <NavbarLink link="#">ссылка 3</NavbarLink>
                    <NavbarLink link="#">ссылка 4</NavbarLink>
                </NavbarCollapse>
            </template>
        </Navbar>
    </header>
</template>

<script setup>
import { Navbar, NavbarLogo, NavbarCollapse, NavbarLink } from 'flowbite-vue'
</script>

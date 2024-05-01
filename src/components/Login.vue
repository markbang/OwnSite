<template>
    <div class="flex flex-col items-center justify-center w-screen h-screen bg-gray-50">
        <div class="w-1/2 p-8 m-4 bg-white shadow-lg register-form rounded-xl">
            <h2 class="flex items-center mb-6 space-x-2 text-2xl font-semibold"><n-icon name="Add-Outline" class="text-gray-500"/><span>注册</span></h2>
            <form @submit.prevent="registerUser" class="">
                <div class="mb-4">
                  <input v-model="register.username" placeholder="输入用户名" required class="w-full h-10 px-3 text-base placeholder-gray-600 border rounded-lg focus:shadow-outline"/>
                </div>
                <div class="mb-6">
                  <input v-model="register.password" type="password" placeholder="输入密码" required class="w-full h-10 px-3 text-base placeholder-gray-600 border rounded-lg focus:shadow-outline" />
               </div>
               <button type="submit" class="w-full h-10 px-3 text-white transition-colors duration-150 bg-blue-600 rounded-lg focus:shadow-outline hover:bg-blue-700">提交注册</button>
            </form>
        </div>
        <div class="w-1/2 p-8 m-4 bg-white shadow-lg login-form rounded-xl">
             <h2 class="flex items-center mb-6 space-x-2 text-2xl font-semibold"><n-icon name="log-in-outline" class="text-gray-500"/><span>登录</span></h2>
             <form @submit.prevent="loginUser" class="">
                 <div class="mb-4">
                    <input v-model="login.username" placeholder="输入用户名" required class="w-full h-10 px-3 text-base placeholder-gray-600 border rounded-lg focus:shadow-outline"/>
                 </div>
                 <div class="mb-6">
                   <input v-model="login.password" type="password" placeholder="输入密码" required class="w-full h-10 px-3 text-base placeholder-gray-600 border rounded-lg focus:shadow-outline" />
                 </div>
                 <button type="submit" class="w-full h-10 px-3 text-white transition-colors duration-150 bg-blue-600 rounded-lg focus:shadow-outline hover:bg-blue-700">提交登录</button>
             </form>
         </div>
    </div>
  </template>
  
  <script lang="ts">
  import { ref, defineComponent } from "vue";
  import { NIcon } from 'naive-ui';
  import { LogInOutline, AddOutline } from '@vicons/ionicons5';
  
  export default defineComponent({
    name: 'AuthForm',
    components: {
      NIcon
    },
    setup() {
      const register = ref({username: '', password: ''});
      const login = ref({username: '', password: ''});
  
      const registerUser = () => {
        console.log(register.value);
        // 这里添加注册逻辑
      };
  
      const loginUser = () => {
        console.log(login.value);
        // 这里添加登录逻辑
      };
  
      return {
        register,
        login,
        registerUser,
        loginUser,
        LogInOutline,
        AddOutline
      }
    }
  })
  </script>
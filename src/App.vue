<template>
  <div id="app">
    <nav class="navbar navbar-default">
      <div class="container-fluid">
        <div class="navbar-header">
          <a class="navbar-brand" href="#">电脑管理系统</a>
        </div>
        <div class="collapse navbar-collapse">
          <ul class="nav navbar-nav">
            <li>
              <router-link to="/">主页</router-link>
            </li>
            <li>
              <router-link to="/about">关于</router-link>
            </li>
          </ul>
          <div class="navbar-text navbar-right">
            <a href="#" title="暂无帮助">帮助</a>
          </div>
        </div>
      </div>
    </nav>
    <router-view></router-view>
  </div>
</template>

<script>
import Vue from 'vue';
import VueRouter from 'vue-router';
import Home from './components/Home';
import About from './components/About';
import Add from './components/Add';
import Detail from './components/Detail';
import Edit from './components/Edit';

Vue.use(VueRouter);

const router = new VueRouter({
  mode: 'history',
  routes: [
    {
      path: '/',
      name: 'home',
      component: Home
    },
    {
      path: '/about',
      name: 'about',
      component: About
    },
    {
      path: '/add',
      name: 'add',
      component: Add
    },
    {
      path: '/detail',
      name: 'detail',
      component: Detail
    },
    {
      path: '/edit',
      name: 'edit',
      component: Edit
    }
  ]
});

export default {
  name: 'App',
  router  
}
</script>

<style>

</style>

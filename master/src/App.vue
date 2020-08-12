<template>
  <div id="container">
    <h2>App 1 container:</h2>
    <div id="app1Container" />
    <h2>App 2 container:</h2>
    <div id="app2Container" />
  </div>
</template>

<script>
  import { registerMicroApps, start } from 'qiankun'

	export default {
    name: 'master',
		data () {
      return {
        apps: [
          { name: 'app-1', entry: '//localhost:8082', container: '#app1Container', activeRule: () => true },
          { name: 'app-2', entry: '//localhost:8083', container: '#app2Container', activeRule: () => true },
        ]
      }
    },
    created () {
      if (!window.__INJECTED_PUBLIC_PATH_BY_QIANKUN__) {
        this.initQiankun()
      } else {
        // fix hot-reload
        location.reload()
      }
    },
		methods: {
			goto (title, href) {
				window.history.pushState({}, title, href)
      },
      initQiankun () {
        registerMicroApps(this.apps)

        start({ singular: false })
      }
		}
	}
</script>

<style scoped>
  #app1Container {
    width: 50%;
    border: 1px solid black;
  }
  #app2Container {
    width: 50%;
    border: 1px solid black;
  }
</style>

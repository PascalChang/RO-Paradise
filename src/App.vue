<template>
  <div id="app">
    <header>
      <h1>RO 掉落物品查詢</h1>
      <p>快速查詢仙境傳說武器掉落來源</p>
    </header>
    <main>
      <ItemTable :items="items" />
    </main>
    <footer>
      <p>資料來源：RO 掉落物品簡易整理表</p>
    </footer>
  </div>
</template>

<script>
import ItemTable from './components/ItemTable.vue'
import itemsData from './data/items.json'

export default {
  name: 'App',
  components: {
    ItemTable
  },
  data() {
    return {
      items: itemsData
    }
  }
}
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  font-family: 'Microsoft JhengHei', 'PingFang TC', 'Helvetica Neue', Arial, sans-serif;
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  min-height: 100vh;
  color: #333;
}

#app {
  max-width: 1200px;
  margin: 0 auto;
  padding: 20px;
  min-height: 100vh;
  display: flex;
  flex-direction: column;
}

header {
  text-align: center;
  margin-bottom: 30px;
  color: white;
}

header h1 {
  font-size: 2.5rem;
  margin-bottom: 10px;
  text-shadow: 2px 2px 4px rgba(0,0,0,0.3);
}

header p {
  font-size: 1.1rem;
  opacity: 0.9;
}

main {
  flex: 1;
}

footer {
  text-align: center;
  margin-top: 30px;
  color: white;
  opacity: 0.8;
  font-size: 0.9rem;
}

@media (max-width: 768px) {
  #app {
    padding: 10px;
  }
  
  header h1 {
    font-size: 2rem;
  }
  
  header p {
    font-size: 1rem;
  }
}
</style> 
<template>
  <div class="item-table">
    <div class="search-section">
      <div class="search-group">
        <label for="search">搜尋：</label>
        <input 
          id="search"
          v-model="searchQuery" 
          placeholder="搜尋物品名稱、職業、掉落魔物..."
          class="search-input"
        />
      </div>
      
      <div class="filter-group">
        <label for="series-filter">武器系列：</label>
        <select id="series-filter" v-model="selectedSeries" class="series-filter">
          <option value="">所有系列</option>
          <option v-for="series in uniqueSeries" :key="series" :value="series">
            {{ series }}
          </option>
        </select>
      </div>
      
      <div class="filter-group">
        <label for="level-filter">等級限制：</label>
        <select id="level-filter" v-model="selectedLevel" class="level-filter">
          <option value="">所有等級</option>
          <option value="1">1級</option>
          <option value="2">2級</option>
          <option value="3">3級</option>
          <option value="4">4級</option>
          <option value="12">12級</option>
          <option value="14">14級</option>
          <option value="16">16級</option>
          <option value="18">18級</option>
          <option value="24">24級</option>
          <option value="27">27級</option>
          <option value="30">30級</option>
          <option value="33">33級</option>
          <option value="無">無限制</option>
        </select>
      </div>
    </div>
    
    <div class="table-container">
      <table class="items-table">
        <thead>
          <tr>
            <th @click="sortBy('名稱')" class="sortable">
              物品名稱
              <span v-if="sortKey === '名稱'" class="sort-icon">
                {{ sortOrder === 'asc' ? '↑' : '↓' }}
              </span>
            </th>
            <th @click="sortBy('職業限制')" class="sortable">
              職業限制
              <span v-if="sortKey === '職業限制'" class="sort-icon">
                {{ sortOrder === 'asc' ? '↑' : '↓' }}
              </span>
            </th>
            <th @click="sortBy('等級限制')" class="sortable">
              等級限制
              <span v-if="sortKey === '等級限制'" class="sort-icon">
                {{ sortOrder === 'asc' ? '↑' : '↓' }}
              </span>
            </th>
            <th @click="sortBy('武器等級')" class="sortable">
              武器等級
              <span v-if="sortKey === '武器等級'" class="sort-icon">
                {{ sortOrder === 'asc' ? '↑' : '↓' }}
              </span>
            </th>
            <th @click="sortBy('系列')" class="sortable">
              系列
              <span v-if="sortKey === '系列'" class="sort-icon">
                {{ sortOrder === 'asc' ? '↑' : '↓' }}
              </span>
            </th>
            <th @click="sortBy('掉落魔物')" class="sortable">
              掉落魔物
              <span v-if="sortKey === '掉落魔物'" class="sort-icon">
                {{ sortOrder === 'asc' ? '↑' : '↓' }}
              </span>
            </th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="item in paginatedItems" :key="item.名稱" class="item-row">
            <td class="item-name">{{ item.名稱 }}</td>
            <td class="job-restriction">{{ item.職業限制 }}</td>
            <td class="level-restriction">{{ item.等級限制 }}</td>
            <td class="weapon-level">{{ item.武器等級 }}</td>
            <td class="series">{{ item.系列 }}</td>
            <td class="monster">{{ item.掉落魔物 }}</td>
          </tr>
        </tbody>
      </table>
    </div>
    
    <div class="pagination">
      <button 
        @click="prevPage" 
        :disabled="currentPage === 1"
        class="page-btn"
      >
        上一頁
      </button>
      <span class="page-info">
        第 {{ currentPage }} 頁，共 {{ totalPages }} 頁
      </span>
      <button 
        @click="nextPage" 
        :disabled="currentPage === totalPages"
        class="page-btn"
      >
        下一頁
      </button>
    </div>
    
    <div class="stats">
      顯示 {{ filteredItems.length }} / {{ items.length }} 個物品
    </div>
  </div>
</template>

<script>
export default {
  name: 'ItemTable',
  props: {
    items: {
      type: Array,
      required: true
    }
  },
  data() {
    return {
      searchQuery: '',
      selectedSeries: '',
      selectedLevel: '',
      sortKey: '名稱',
      sortOrder: 'asc',
      currentPage: 1,
      itemsPerPage: 20
    }
  },
  computed: {
    uniqueSeries() {
      return [...new Set(this.items.map(item => item.系列))].sort()
    },
    filteredItems() {
      return this.items.filter(item => {
        const matchesSearch = !this.searchQuery || 
          item.名稱.toLowerCase().includes(this.searchQuery.toLowerCase()) ||
          item.職業限制.toLowerCase().includes(this.searchQuery.toLowerCase()) ||
          item.掉落魔物.toLowerCase().includes(this.searchQuery.toLowerCase())
        
        const matchesSeries = !this.selectedSeries || item.系列 === this.selectedSeries
        const matchesLevel = !this.selectedLevel || item.等級限制 === this.selectedLevel
        
        return matchesSearch && matchesSeries && matchesLevel
      })
    },
    sortedItems() {
      return [...this.filteredItems].sort((a, b) => {
        let aVal = a[this.sortKey]
        let bVal = b[this.sortKey]
        
        // 處理等級限制的排序
        if (this.sortKey === '等級限制') {
          if (aVal === '無') aVal = 0
          if (bVal === '無') bVal = 0
          aVal = parseInt(aVal) || 0
          bVal = parseInt(bVal) || 0
        }
        
        if (this.sortOrder === 'asc') {
          return aVal > bVal ? 1 : -1
        } else {
          return aVal < bVal ? 1 : -1
        }
      })
    },
    totalPages() {
      return Math.ceil(this.sortedItems.length / this.itemsPerPage)
    },
    paginatedItems() {
      const start = (this.currentPage - 1) * this.itemsPerPage
      const end = start + this.itemsPerPage
      return this.sortedItems.slice(start, end)
    }
  },
  watch: {
    searchQuery() {
      this.currentPage = 1
    },
    selectedSeries() {
      this.currentPage = 1
    },
    selectedLevel() {
      this.currentPage = 1
    }
  },
  methods: {
    sortBy(key) {
      if (this.sortKey === key) {
        this.sortOrder = this.sortOrder === 'asc' ? 'desc' : 'asc'
      } else {
        this.sortKey = key
        this.sortOrder = 'asc'
      }
    },
    prevPage() {
      if (this.currentPage > 1) {
        this.currentPage--
      }
    },
    nextPage() {
      if (this.currentPage < this.totalPages) {
        this.currentPage++
      }
    }
  }
}
</script>

<style scoped>
.item-table {
  background: white;
  border-radius: 12px;
  box-shadow: 0 4px 20px rgba(0,0,0,0.15);
  overflow: hidden;
}

.search-section {
  padding: 20px;
  background: linear-gradient(135deg, #f5f7fa 0%, #c3cfe2 100%);
  display: grid;
  grid-template-columns: 2fr 1fr 1fr;
  gap: 20px;
  align-items: end;
}

.search-group, .filter-group {
  display: flex;
  flex-direction: column;
  gap: 8px;
}

.search-group label, .filter-group label {
  font-weight: 600;
  color: #333;
  font-size: 0.9rem;
}

.search-input, .series-filter, .level-filter {
  padding: 12px;
  border: 2px solid #e1e5e9;
  border-radius: 8px;
  font-size: 14px;
  transition: all 0.3s ease;
  background: white;
}

.search-input:focus, .series-filter:focus, .level-filter:focus {
  outline: none;
  border-color: #667eea;
  box-shadow: 0 0 0 3px rgba(102, 126, 234, 0.1);
}

.table-container {
  overflow-x: auto;
}

.items-table {
  width: 100%;
  border-collapse: collapse;
  background: white;
}

.items-table th,
.items-table td {
  padding: 15px 12px;
  text-align: left;
  border-bottom: 1px solid #e1e5e9;
}

.items-table th {
  background: #f8f9fa;
  font-weight: 600;
  color: #495057;
  position: sticky;
  top: 0;
  z-index: 10;
}

.sortable {
  cursor: pointer;
  user-select: none;
  transition: background-color 0.2s ease;
}

.sortable:hover {
  background: #e9ecef !important;
}

.sort-icon {
  margin-left: 5px;
  color: #667eea;
  font-weight: bold;
}

.item-row:hover {
  background: #f8f9fa;
  transform: translateY(-1px);
  box-shadow: 0 2px 8px rgba(0,0,0,0.1);
  transition: all 0.2s ease;
}

.item-name {
  font-weight: 600;
  color: #2c3e50;
}

.job-restriction {
  color: #6c757d;
  font-size: 0.9rem;
}

.level-restriction, .weapon-level {
  text-align: center;
  font-weight: 600;
  color: #495057;
}

.series {
  color: #667eea;
  font-weight: 600;
}

.monster {
  color: #dc3545;
  font-weight: 500;
}

.pagination {
  display: flex;
  justify-content: center;
  align-items: center;
  gap: 20px;
  padding: 20px;
  background: #f8f9fa;
  border-top: 1px solid #e1e5e9;
}

.page-btn {
  padding: 8px 16px;
  border: 2px solid #667eea;
  background: white;
  color: #667eea;
  border-radius: 6px;
  cursor: pointer;
  font-weight: 600;
  transition: all 0.3s ease;
}

.page-btn:hover:not(:disabled) {
  background: #667eea;
  color: white;
}

.page-btn:disabled {
  opacity: 0.5;
  cursor: not-allowed;
}

.page-info {
  color: #6c757d;
  font-weight: 500;
}

.stats {
  padding: 15px;
  background: #e9ecef;
  text-align: center;
  color: #495057;
  font-weight: 500;
  border-top: 1px solid #dee2e6;
}

@media (max-width: 768px) {
  .search-section {
    grid-template-columns: 1fr;
    gap: 15px;
  }
  
  .items-table th,
  .items-table td {
    padding: 10px 8px;
    font-size: 0.9rem;
  }
  
  .pagination {
    flex-direction: column;
    gap: 10px;
  }
  
  .job-restriction {
    font-size: 0.8rem;
  }
}
</style> 
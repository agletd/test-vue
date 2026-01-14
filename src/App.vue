<template>
  <div class="container">
    <div class="top-section">
      <!-- Верхний левый блок - выбранные вещи пользователя -->
      <div class="selected-user-items">
        <div class="items-grid">
          <div 
            v-for="item in selectedUserItems.slice(0, 2)" 
            :key="item.id"
            class="item-box"
          >
            {{ item.name }}
          </div>
        </div>
        <div class="counter">
          selected: {{ selectedUserItems.length }} / 6
        </div>
      </div>

      <!-- Верхний правый блок - выбранная вещь -->
      <div class="selected-choice-item">
        <div class="selected-text">
          {{ selectedChoiceItem ? selectedChoiceItem.name : 'SELECTED ITEM' }}
        </div>
      </div>
    </div>

    <div class="bottom-section">
      <!-- Нижний левый блок - вещи пользователя -->
      <div class="user-items-container">
        <div class="items-grid-4">
          <div 
            v-for="item in userItems" 
            :key="item.id"
            class="item-box clickable"
            :class="{ selected: isUserItemSelected(item) }"
            @click="toggleUserItem(item)"
          >
            {{ item.name }}
          </div>
        </div>
      </div>

      <!-- Нижний правый блок - вещи на выбор -->
      <div class="choice-items-container">
        <div class="items-grid-4">
          <div 
            v-for="item in choiceItems" 
            :key="item.id"
            class="item-box clickable"
            :class="{ 'selected-green': selectedChoiceItem?.id === item.id }"
            @click="toggleChoiceItem(item)"
          >
            {{ item.name }}
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'App',
  data() {
    return {
      selectedUserItems: [],
      selectedChoiceItem: null,
      userItems: [
        { id: 1, name: "Shoes 1" },
        { id: 2, name: "Shoes 2" },
        { id: 3, name: "Shoes 3" },
        { id: 4, name: "Shoes 4" },
        { id: 5, name: "T-shirt 1" },
        { id: 6, name: "T-shirt 2" },
        { id: 7, name: "T-shirt 3" },
        { id: 8, name: "T-shirt 4" }
      ],
      choiceItems: [
        { id: 11, name: "Jacket 1" },
        { id: 12, name: "Jacket 2" },
        { id: 13, name: "Jacket 3" },
        { id: 14, name: "Jacket 4" },
        { id: 15, name: "Hoodie 1" },
        { id: 16, name: "Hoodie 2" },
        { id: 17, name: "Hoodie 3" },
        { id: 18, name: "Hoodie 4" }
      ]
    }
  },
  methods: {
    toggleUserItem(item) {
      const index = this.selectedUserItems.findIndex(i => i.id === item.id);
      
      if (index !== -1) {
        // Убираем из выбранных
        this.selectedUserItems.splice(index, 1);
      } else {
        // Добавляем, если меньше 6
        if (this.selectedUserItems.length < 6) {
          this.selectedUserItems.push(item);
        }
      }
    },
    toggleChoiceItem(item) {
      if (this.selectedChoiceItem?.id === item.id) {
        this.selectedChoiceItem = null;
      } else {
        this.selectedChoiceItem = item;
      }
    },
    isUserItemSelected(item) {
      return this.selectedUserItems.some(i => i.id === item.id);
    }
  }
}
</script>

<style>
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

.container {
  padding: 40px;
  background: #f0f0f0;
  min-height: 100vh;
}

.top-section,
.bottom-section {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 40px;
  margin-bottom: 40px;
}

.selected-user-items,
.selected-choice-item,
.user-items-container,
.choice-items-container {
  background: white;
  border: 4px solid black;
  padding: 30px;
}

.items-grid {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 20px;
  margin-bottom: 20px;
}

.items-grid-4 {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 20px;
}

.item-box {
  border: 2px solid black;
  padding: 20px;
  text-align: center;
  background: white;
}

.item-box.clickable {
  cursor: pointer;
  transition: background 0.2s;
}

.item-box.clickable:hover {
  background: #e0e0e0;
}

.item-box.selected {
  background: #a3d5ff;
}

.item-box.selected-green {
  background: #a3ffb3;
}

.counter {
  text-align: center;
  font-weight: bold;
  font-size: 16px;
}

.selected-choice-item {
  display: flex;
  align-items: center;
  justify-content: center;
}

.selected-text {
  font-size: 28px;
  font-weight: bold;
  text-align: center;
}
</style>
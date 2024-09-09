<template>
  <div class="app">
    <h1 class="header">Telepod QR Codes</h1>

    <!-- Search bar -->
    <input 
      type="text" 
      v-model="searchQuery" 
      placeholder="Search by name, ID, or side" 
      class="search-bar"
    />

    <div class="item-list">
      <div v-for="item in filteredItems" :key="item.id" class="item-box">
        <!-- Name at the top -->
        <h3 class="item-name">{{ item.name }}</h3>

        <!-- Images in a flex container -->
        <div class="item-images">
          <!-- First image (Character image) -->
          <img v-if="item.img && item.img[0]" :src="item.img[0]" :alt="`${item.name} image`" class="main-img" />
          
          <!-- QR code (second image) -->
          <img v-if="item.img && item.img[1]" :src="item.img[1]" :alt="`${item.name} QR code`" class="qr-img" />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { items } from './data.js';

export default {
  data() {
    return {
      items,
      searchQuery: '',
    };
  },
  computed: {
    filteredItems() {
      const query = this.searchQuery.toLowerCase();
      return this.items.filter(item => {
        const nameMatch = item.name && item.name.toLowerCase().includes(query);
        const idMatch = item.id && item.id.toString().includes(query);
        const sideMatch = item.side && item.side.toLowerCase().includes(query);
        return nameMatch || idMatch || sideMatch;
      });
    },
  },
};
</script>

<style scoped>
/* General app container styling */
.app {
  max-width: 100%;
  margin: 0 auto;
  padding: 10px;
  box-sizing: border-box;
  background-color: #333; /* Background color for contrast */
}

/* Header styling */
.header {
  color: white;
  text-align: center;
  margin-bottom: 20px;
}

/* Style for the overall item list */
.item-list {
  display: flex;
  flex-direction: column;
  gap: 20px;
}

/* Style for each box (item) */
.item-box {
  border: 1px solid #ccc;
  border-radius: 8px;
  padding: 15px;
  background-color: #444; /* Slightly darker background for items */
  max-width: 100%;
  box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
}

/* Style for the item name */
.item-name {
  font-size: 18px;
  text-align: center;
  color: white; /* White text color */
  margin-bottom: 10px;
}

/* Flex container for the images */
.item-images {
  display: flex;
  flex-direction: row;
  gap: 10px;
  justify-content: center;
}

/* Main image style */
.main-img {
  max-width: 60%;
  height: auto;
  border-radius: 8px;
}

/* QR image style */
.qr-img {
  max-width: 30%;
  height: auto;
  border-radius: 8px;
}

/* Style for the search bar */
.search-bar {
  width: 100%;
  padding: 10px;
  margin-bottom: 20px;
  border: 1px solid #ccc;
  border-radius: 4px;
  background-color: #555; /* Dark background for the search bar */
  color: white; /* White text color for the search bar */
}

/* Responsive design for different devices */
@media (max-width: 767px) {
  .item-box {
    padding: 10px;
  }

  .item-name {
    font-size: 16px;
  }

  .main-img {
    max-width: 55%;
  }

  .qr-img {
    max-width: 35%;
  }
}

@media (min-width: 768px) and (max-width: 1024px) {
  .item-box {
    padding: 15px;
  }

  .item-name {
    font-size: 18px;
  }

  .main-img {
    max-width: 60%;
  }

  .qr-img {
    max-width: 30%;
  }
}
</style>

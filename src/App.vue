<template>
  <div class="app">
    <h1> Food Catalogue</h1>

    <!-- Product List -->
    <div class="product-list">
      <ProductCard
        v-for="product in products"
        :key="product.id"
        :product="product"
        :saved="isSaved(product.id)"
        @toggle-save="toggleSave"
      />
    </div>

    <!-- Saved Items -->
    <h2> Saved Items</h2>
    <div v-if="savedItems.length" class="saved-list">
      <ProductCard
        v-for="product in savedItems"
        :key="product.id"
        :product="product"
        :saved="true"
        @toggle-save="toggleSave"
      />
    </div>
    <p v-else>No saved items yet.</p>
  </div>
</template>

<script>
import ProductCard from "./components/ProductCard.vue";

export default {
  name: "App",
  components: { ProductCard },
  data() {
    return {
      products: [
      {         
      id:1,
      name: "Spaghetti",
      description: "Classic Italian Pasta with rich meat sauce.",
      chef: "Gordan Ramsey",
      level: "*****",  /*chef level in stars max being 5 star */
      price: 165.00,
      available: "",
      image:"https://www.servingdumplings.com/wp-content/uploads/2023/01/the-best-spicy-spaghetti-bolognese-4-75b75f26.jpg"
      },
      {         
      id:2,
      name: "Croissant",
      chef: "Ratatouille",
      level: "**",
      price: 80.00,
      description: "nicely sixed croissant with chocolate spread inside",
      available: "SOLD OUT",
      image:"https://www.theflavorbender.com/wp-content/uploads/2020/05/French-Croissants-SM-2363.jpg"
      },
      {       
      id:3,
      name: "Chicken Soup",
      chef: "Thauhier",
      level: "*",
      price: 120.00,
      description: "Nice and warm Chicken Soup fresh.",
      available: "",
      image:"https://theforkedspoon.com/wp-content/uploads/2019/12/Chicken-Soup-6-1.jpg"
      },
      {       
      id:4,
      name: "Briyani",
      chef: "Random Indian guy",
      level: "***",
      price: 145.00,
      description: "Freshly cooked Briyani",
      available: "SOLD OUT",
      image:"https://i.pinimg.com/originals/aa/a9/2a/aaa92a3c0a605671a2e1b20871913c34.jpg"
      },
      {       
      id:5,
      name: "Chocolate Cake",
      chef: "Cake Boss",
      level: "*****",
      price: 225.00,
      description: "Best cake baked by the best Baker",
      available: "",
      image:"https://www.bunsenburnerbakery.com/wp-content/uploads/2023/09/best-chocolate-layer-cake-41.jpg"
      },
      {       
      id:6,
      name: "Mac and Cheese",
      chef: "Gordan Ramsey",
      level: "*****",
      price: 200.00,
      description: "Maccaroni coated with the most flavourable cheese.",
      available: "",
      image:"https://www.allrecipes.com/thmb/e8uotDI18ieXNBY0KpmtGKbxMRM=/1500x0/filters:no_upscale():max_bytes(150000):strip_icc()/238691-Simple-Macaroni-And-Cheese-mfs_008-4x3-6ed91ba87a1344558aacc0f9ef0f4b41.jpg"
      },
      ],
      savedIds: [],
    };
  },
  computed: {
    savedItems() {
      return this.products.filter(p => this.savedIds.includes(p.id));
    }
  },
  created() {
    // load saved ids from localStorage
    const saved = localStorage.getItem("savedItems");
    if (saved) {
      try {
        this.savedIds = JSON.parse(saved);
      } catch {
        this.savedIds = [];
      }
    }
  },
  methods: {
    isSaved(id) {
      return this.savedIds.includes(id);
    },
    toggleSave(id) {
      if (this.isSaved(id)) {
        this.savedIds = this.savedIds.filter(savedId => savedId !== id);
      } else {
        this.savedIds.push(id);
      }
      localStorage.setItem("savedItems", JSON.stringify(this.savedIds));
    }
  }
};
</script>

<style>
.app {
  font-family: Arial, sans-serif;
  padding: 20px;
}
.product-list, .saved-list {
  display: flex;
  gap: 15px;
  flex-wrap: wrap;
}
</style>
<template>
<el-form ref="form" :model="form" label-width="120px">
  <el-row :gutter="20">
    <el-col :span="18">
      <el-form-item label="Title">
        <el-input v-model="title"></el-input>
      </el-form-item>
    </el-col>
    <el-col :span="6">
      <el-form-item label="Price">
        <el-input v-model="price"></el-input>
      </el-form-item>
    </el-col>
  </el-row>
  <el-form-item label="Description">
    <el-input type="textarea" v-model="description"></el-input>
  </el-form-item>
  <el-form-item>
    <el-button type="primary" @click="create">Submit</el-button>
    <el-button>Cancel</el-button>
  </el-form-item>
</el-form>
</template>

<script>
export default {
  data() {
    return {
      form: {
        title: '',
        description: '',
        price: ''
      }
    }
  },

  computed: {

    product: {
      get() {
        return this.$store.state.product;
      }
    },

    title: {
      get() {
        return this.$store.state.product.title;
      },

      /**
       * @param title
       */
      set(title) {
        this.$store.dispatch('setProductTitle', title);
      }
    },

    description: {
      get() {
        return this.$store.state.product.description;
      },

      /**
       * @param description
       */
      set(description) {
        this.$store.dispatch('setProductDescription', description);
      }
    },

    price: {
      get() {
        return this.$store.state.product.price;
      },

      /**
       * @param price
       */
      set(price) {
        this.$store.dispatch('setProductPrice', price);
      }
    }
  },

  methods: {
    create() {
      this.$store.dispatch('saveProduct', this.product).then(() => {
        this.$message({
          message: 'Congrats, you have created a product.',
          type: 'success'
        });
        
        this.$store.dispatch('getProducts');
      });
    }
  }
}
</script>

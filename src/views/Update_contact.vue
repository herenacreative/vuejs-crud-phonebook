<template>
    <div>
    <el-card class="box-card" style="text-align: center;">
      <el-breadcrumb separator="/">
        <el-breadcrumb-item :to="{ path: '/contact' }">contact</el-breadcrumb-item>
        <el-breadcrumb-item>Update Contact</el-breadcrumb-item>
      </el-breadcrumb>
    
       <el-form :model="userData">

            <el-form-item label="Name">
              <el-input v-model="userData.name">  </el-input>
            </el-form-item>

            <el-form-item label="Address">
              <el-input v-model="userData.address">  </el-input>
            </el-form-item>

            <el-form-item label="Phone">
              <el-input v-model="userData.phone"></el-input>
            </el-form-item>

            <el-form-item>
                <el-button @click="edit(id)" size="small">
                  update
                </el-button>
            </el-form-item>

       </el-form>
    </el-card>
    </div>
</template>

<script>
  import axios from "axios" 

  export default {
    data() {
      return {
        userData: {
            name: "",
            address: "",
            phone:""
            
        }
      }
    },
    created() {
      this.getContacts()
    }, 
    methods: {
      getContacts: async function() {
        const id = this.$route.params.id
        const {data} = await axios.get(`https://address-book-exp-api.herokuapp.com/users/${id}`);
        this.userData = data;  
        console.log(data, "HREEE", id, "HEREE")
      },
      edit: async function() {
        const id = this.$route.params.id
        const {data} = await axios.patch(`https://address-book-exp-api.herokuapp.com/users/${id}`,{           
            name: this.userData.name,
            address:this.userData.address,
            phone: this.userData.phone
        });
        console.log(id)
      }
    }
  }
</script>


<style>
  .box-card {
    width: 480px;
    margin: 50px auto;
  }
</style>
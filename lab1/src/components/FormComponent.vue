<template >
  <div>
    <button class="continue-application" @click="handleButton" name="form">
      Reigster
    </button>
    <button @click="handleButton" name="admins">
      <i class="bi bi-person-fill-gear"></i>
      Admins
    </button>
    <button @click="handleButton" name="users">
      <i class="bi bi-person-fill"></i>
      Users
    </button>
    <div v-if="activeFlag === 'form'" class="container mt-5 text-center py-5">
      <div class="form-container mx-auto">
        <p class="title">Register</p>
        <form class="form" action="" @submit.prevent="formHandling">
          <div class="input-group mb-3">
            <label for="username">Username</label>
            <input type="text" name="username" id="username" placeholder="" v-model="person.name">
          </div>
          <div class="input-group mb-3">
            <label for="email">Email</label>
            <input type="email" name="email" id="email" placeholder="" v-model="person.email">
          </div>
          <div class="radio-inputs mb-3">
            <label class="radio">
              <input type="radio" name="radio" value="admin" checked="" v-model="selectedOption">
              <span class="name">Admin</span>
            </label>
            <label class="radio">
              <input type="radio" name="radio" value="user" v-model="selectedOption">
              <span class="name">User</span>
            </label>
          </div>
          <button class="sign" type="submit">Register</button>
        </form>
      </div>
    </div>
    <AdminComponent v-if="activeFlag === 'admins'" :admins="getAdmins" @deleteAdmin="deletePerson"></AdminComponent>
    <UserComponent v-if="activeFlag === 'users'" :users="getUsers" @deleteUser="deletePerson"></UserComponent>
    
  </div>
</template>
<script>
import AdminComponent from "./AdminComponent.vue";
import UserComponent from "./UserComponent.vue";

export default {
  name: "FormComponent",
  data() {
    return {
      activeFlag: "form",
      selectedOption:"admin",
      person: {
        name: '',
        email: '',
        role:''
      },
      persons: [
        {
          name: "Habiba",
          email: "habiba@gmail.com",
          role: "admin",
        },
        {
          name: "Ahmed",
          email: "ahmed@gmail.com",
          role: "user",
        },
        {
          name: "Aya",
          email: "aya@gmail.com",
          role: "user",
        },
        {
          name: "Mohamed",
          email: "mohamed@gmail.com",
          role: "admin",
        },
      ],
    };
  },
  methods: {
    handleButton(e) {
      this.activeFlag = e.target.name;
      console.log(this.activeFlag);
    },
    formHandling() {
      console.log(this.person)
      this.person.role=this.selectedOption;
      this.persons.push(this.person)
      console.log(this.persons)
      this.person={
        name:"",
        email:"",
        role:""
      };
    },
    deletePerson(email)
    {
      this.persons =  this.persons.filter((person)=> person.email !== email);
      //      this.persons =  this.persons.filter((person,index)=> index !== deletedIndex);

    }
  },
  computed: {
    getAdmins() {
      return this.persons.filter((person) => person.role === "admin");
    },
    getUsers() {
      return this.persons.filter((person) => person.role === "user");
    },
  },
  components: {
    AdminComponent,
    UserComponent,
  },
};
</script>
<style scoped>
.continue-application {
  --color: #fff;
  --background: #404660;
  --background-hover: #3a4059;
  --background-left: #2b3044;
  border: none;
  outline: none;
  cursor: pointer;
  position: relative;
  border-radius: 5px;
  font-size: 14px;
  font-weight: 500;
  line-height: 19px;
  -webkit-appearance: none;
  -webkit-tap-highlight-color: transparent;
  transition: background 0.3s;
  color: var(--color);
  background: var(--bg, var(--background));
}


button {
  display: inline-block;
  border-radius: 4px;
  background-color: #3d405b;
  border: none;
  color: #ffffff;
  text-align: center;
  font-size: 14px;
  font-weight: 500;
  line-height: 19px;
  padding: 16px;
  width: 130px;
  transition: all 0.5s;
  cursor: pointer;
  margin: 5px;
}

button i {
  cursor: none;
  display: inline-block;
  position: relative;
  transition: 0.5s;
}

button i:after {
  content: "";
  position: absolute;
  opacity: 0;
  top: 0;
  right: -15px;
  transition: 0.5s;
}

button:hover i {
  padding-right: 15px;
}

button:hover i:after {
  opacity: 1;
  right: 0;
}


.form-container {
  width: 320px;
  border-radius: 0.75rem;
  background-color: rgba(17, 24, 39, 1);
  padding: 2rem;
  color: rgba(243, 244, 246, 1);
}

.title {
  text-align: center;
  font-size: 1.5rem;
  line-height: 2rem;
  font-weight: 700;
}

.form {
  margin-top: 1.5rem;
}

.input-group {
  margin-top: 0.25rem;
  font-size: 0.875rem;
  line-height: 1.25rem;
}

.input-group label {
  display: block;
  color: rgba(156, 163, 175, 1);
  margin-bottom: 4px;
}

.input-group input {
  width: 100%;
  border-radius: 0.375rem;
  border: 1px solid rgba(55, 65, 81, 1);
  outline: 0;
  background-color: rgba(17, 24, 39, 1);
  padding: 0.75rem 1rem;
  color: rgba(243, 244, 246, 1);
}

.input-group input:focus {
  border-color: rgba(167, 139, 250);
}

.sign {
  display: block;
  width: 100%;
  background-color: rgba(167, 139, 250, 1);
  padding: 0.75rem;
  text-align: center;
  color: rgba(17, 24, 39, 1);
  border: none;
  border-radius: 0.375rem;
  font-weight: 600;
}
.radio-inputs {
  position: relative;
  display: flex;
  flex-wrap: wrap;
  border-radius: 0.5rem;
  background-color: #fff;
  box-sizing: border-box;
  box-shadow: 0 0 0px 1px rgba(0, 0, 0, 0.06);
  padding: 0.25rem;
  width: 100%;
  font-size: 14px;
}

.radio-inputs .radio {
  flex: 1 1 auto;
  text-align: center;
}

.radio-inputs .radio input {
  display: none;
}

.radio-inputs .radio .name {
  display: flex;
  cursor: pointer;
  align-items: center;
  justify-content: center;
  border-radius: 0.5rem;
  border: none;
  padding: .5rem 0;
  color: rgba(51, 65, 85, 1);
  transition: all .15s ease-in-out;
}

.radio-inputs .radio input:checked + .name {
  background-color: rgba(243, 244, 246, 1);
  font-weight: 600;
}
</style>
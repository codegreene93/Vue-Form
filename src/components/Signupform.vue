<template>
  <form @submit.prevent="handleSubmit">
      <label>Email</label>
      <input type="email" required v-model="email">

      <label>Password</label>
      <input type="password" required v-model="password">
      <div v-if="passwordError">{{passwordError}}</div>

      <label>Role: </label>
      <select v-model="role">
          <option value="developer">Web Developer</option>
          <option value="designer">Web Designer</option>
      </select>

      <label>Skills: </label>
      <input type="text" v-model="tempSkill" @keyup.alt="addSkill">
      <div v-for="skill in skills" :key="skill">
         <button id="deleteButton" @click="removeSkill(skill)">{{skill}}</button> 
      </div>

      <div class="terms">
          <input type="checkbox" v-model="terms" required>
          <label>Accept Terms and Conditions</label>
      </div>

      <button class="submit">Submit</button>
  </form>
 
</template>

<script>
export default {
    data (){
        return{
            email: '',
            password: '',
            role: '',
            terms: false,
           tempSkill: '',
           skills: [],
           passwordError: ''
        }
    },
    methods: {
        addSkill(e){
            if(e.key === ',' && this.tempSkill){
                if(!this.skills.includes(this.tempSkill)){
                    this.skills.push(this.tempSkill)
                }
                this.tempSkill = ''
            }
        },
        removeSkill(skill){
            this.skills = this.skills.filter((item) =>{
              return  skill !== item;
            })
        },
        handleSubmit() {
            this.passwordError = this.password.length > 5 ? '' : 'Password must be at least 6 charecters long'
            if(!this.passwordError){
                console.log('Submit successful')
            }
        }
    }
}
</script>

<style>
form {
    max-width: 420px;
    margin: 30px auto;
    background: #fff;
    text-align: left;
    padding: 40px;
    border-radius: 10px;
}

label{
    color: #aaa;
    display: inline-block;
    margin: 25px 0 15px;
    font-size: 0.6em;
    text-transform: uppercase;
    letter-spacing: 1px;
    font-weight: bold;
}
input, select {
    display: block;
    padding: 10px 6px;
    width: 100%;
    box-sizing: border-box;
    border:none;
    border-bottom: 1px solid #ddd;
}
input[type="checkbox"] {
    display: inline-block;
    width: 16px;
    margin: 0 10px 0 0;
    position: relative;
    top: 2px;
}

#deleteButton{
    display: inline-block;
    background: rgb(238, 226, 226);
    border-radius: 20px;
    border: none;
    font-weight: bold;
    color: #aaa;
    padding: 0 10px;
}
.submit {
    background: #0b6dff;
    border:0;
    padding: 10px 20px;
    color: white;
    border-radius: 20px;
}

</style>
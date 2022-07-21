<template>
  <form @submit="handleSubmit">
    <h3>Signup Form</h3>
    <label>Email:</label>
    <input type="email" required v-model="email"/>

    <label>Password:</label>
    <input type="password" required v-model="password" @focus="clearError"/>
    <div v-if="passwordError" class="error">{{passwordError}}</div>

    <label>Role:</label>
    <select v-model="role">
      <option value="developer">Web Developer</option>
      <option value="designer">Web Designer</option>
    </select>

    <label>Languages:</label>
    <div class="language">
      <input type="checkbox" value="english" v-model="languages"/>
      <label>English</label>
    </div>
    <div class="language">
      <input type="checkbox" value="japanese" v-model="languages"/>
      <label>Japanese</label>
    </div>
    <div class="language">
      <input type="checkbox" value="vietnamese" v-model="languages"/>
      <label>Vietnammese</label>
    </div>

    <label>Skills (press Alt + ',' after each skill was entered):</label>
    <input type="text" v-model="tempSkill" @keyup.alt="addSkill"/>
    <div v-for="skill in skills" :key="skill" class="pill">
      <span @click="deleteSkill(skill)">{{skill}}</span>
    </div>

    <div class="terms">
      <input type="checkbox" required v-model="terms"/>
      <label>Accept terms and conditions</label>
    </div>

    <div class="submit">
      <button>Create an Account</button>
    </div>
  </form>

  <div v-if="success">
    <p>Email: {{email}}</p>
    <p>Password: {{password}}</p>
    <p>Role: {{role}}</p>
    <p>Terms accepted: {{terms}}</p>
    <div>
      <span>Languages checked:</span>
      <div v-for="(name, index) in names" :key="index">
        <div>{{name}}</div>
      </div>
    </div>
  </div>
  
</template>

<script>
export default {
  name: 'SingupForm',
  data() {
    return {
      email: '',
      password: '',
      role: 'developer',
      terms: false,
      languages: [],
      tempSkill: '',
      skills: [],
      passwordError: '',
      success: false
    }
  },
  methods: {
    addSkill(e) {
      if (e.key === ',' && this.tempSkill) {
        if (!this.skills.includes(this.tempSkill)) {
          this.skills.push(this.tempSkill)
        }
        this.tempSkill = ''
      }
    },
    deleteSkill(skill) {
      this.skills = this.skills.filter((item) => item !== skill)
    },
    handleSubmit(e) {
      e.preventDefault();
      // validate password
      this.passwordError = this.password.length > 5 ? '' : 'Password must be at least 6 chars long'
      if (!this.passwordError) {
        this.success = true
      }
    },
    clearError() {
      console.log('ssss')
      this.passwordError = ''
    }
  }
}
</script>

<style scoped>
form {
  max-width: 420px;
  margin: 30px auto;
  background: white;
  padding: 40px;
  border-radius: 10px;
}
label {
  color: #aaa;
  display: inline-block;
  margin: 25px 0 15px;
  font-size: 0.6em;
  text-transform: uppercase;
  letter-spacing: 1px;
  font-weight: bold;
  text-align: start;
  width: 100%;
}
input, select {
  display: block;
  padding: 10px 6px;
  width: 100%;
  box-sizing: border-box;
  border: none;
  border-bottom: 1px solid #ddd;
  color: #555;
  outline: none;
}
input[type="checkbox"] {
  display: inline-block;
  width: 16px;
  margin: 0 10px 0 0;
  position: relative;
  top: 2px;
}
.terms, .language {
  display: flex;
  align-items: center;
}
.language {
  margin-bottom: 16px;
}
.language label {
  margin: 0;
}
.pill {
  display: inline-block;
  margin: 20px 10px 0 0;
  padding: 6px 12px;
  background: #eee;
  border-radius: 20px;
  font-size: 12px;
  letter-spacing: 1px;
  font-weight: bold;
  color: #777;
  cursor: pointer;
}
.submit {
  text-align: center;
}
button {
  background: #0b6dff;
  border: 0;
  padding: 10px 20px;
  margin-top: 20px;
  color: white;
  border-radius: 20px;
  cursor: pointer;
}
button:hover {
  opacity: 0.8;
}
.error {
  color: #ff0062;
  font-size: 0.8em;
  margin-top: 10px;
  font-weight: bold;
  text-align: start;
}
</style>

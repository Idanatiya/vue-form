<template>
  <form @submit.prevent="submitForm">
    <label for="">Email</label>
    <input required v-model="email" type="email" />
    <label for="">Password</label>
    <input required v-model="password" type="password" />
    <div v-if="passwordError">
      {{ passwordError }}
    </div>
    <label for="">Role</label>
    <select v-model="role">
      <option value="" disabled>Choose Role</option>
      <option value="developer">Developer</option>
      <option value="designer">Designer</option>
    </select>
    <div>
      <label for="">Skills</label>
      <input @keyup.enter="addSkill" type="text" v-model="tempSkill" />
      <p>{{ tempSkill }}</p>
      <div class="skills" v-if="skills.length">
        <div
          class="skill"
          @click="deleteSkill(skill)"
          :key="index"
          v-for="(skill, index) in skills"
        >
          <span>
            {{ skill }}
          </span>
        </div>
      </div>
    </div>
    <div class="terms">
      <input v-model="terms" type="checkbox" required />
      <label for="">Accpet terms and conditions</label>
    </div>
    <!-- <div>
      <input type="checkbox" value="ninja" v-model="names" />
      <label for="">Ninja</label>
    </div>
    <div>
      <input type="checkbox" value="smuarai" v-model="names" />
      <label for="">Smuarai</label>
    </div>
    <div>
      <input type="checkbox" value="bandit" v-model="names" />
      <label for="">Bandit</label>
    </div> -->
    <div class="submit">
      <button>Create an Account</button>
    </div>
  </form>
  <p :key="item" v-for="item in [email, password, role, terms, names, skills]">
    {{ item.toString().toUpperCase() }} - {{ item }}
  </p>
</template>

<script>
export default {
  data() {
    return {
      email: "",
      password: "",
      role: "",
      terms: false,
      tempSkill: "",
      skills: [],
      names: [],
      passwordError: "",
    };
  },
  methods: {
    addSkill(ev) {
      if (this.skills.includes(this.tempSkill)) return;
      this.skills.unshift(this.tempSkill);
      this.tempSkill = "";
    },
    deleteSkill(skill) {
      this.skills = this.skills.filter(
        (currSkill) => currSkill.toLowerCase() !== skill.toLowerCase()
      );
      console.log({ skill });
    },
    submitForm(ev) {
      this.passwordError =
        this.password.length > 5 ? "" : "Password must be at least 6 chars";
      if (!this.passwordError) {
        console.log("Pass form validation");
      }
    },
  },
};
</script>

<style>
form {
  max-width: 420px;
  margin: 30px auto;
  background: white;
  text-align: left;
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
}
input,
select {
  display: block;
  padding: 10px 6px;
  width: 100%;
  box-sizing: border-box;
  border: none;
  border-bottom: 1px solid #ddd;
  color: #555;
}

input[type="checkbox"] {
  display: inline-block;
  width: 16px;
  margin: 0 10px 0 0;
  position: relative;
  top: 2px;
}

.skills {
  margin-top: 10px;
  display: flex;
  flex-wrap: wrap;
}
.skill {
  background: #eee;
  border-radius: 20px;
  display: inline;
  margin: 4px;
  padding: 5px 7px;
  letter-spacing: 1px;
  font-weight: bold;
  color: #777;
  cursor: pointer;
}

.skill:hover {
  opacity: 0.8;
}

button {
  background: #0b6dff;
  border: none;
  padding: 10px 20px;
  color: #fff;
  border-radius: 10px 20px;
}

.submit {
  text-align: center;
}
</style>

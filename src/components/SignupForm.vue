<template>
  <form @submit.prevent="handleSubmit">
    <h1>Example Form</h1>
    <label>Email</label>
    <input v-model="email" type="email" required />
    <label>Password</label>
    <input v-model="password" type="password" required />
    <div v-if="passwordError" class="error">{{ passwordError }}</div>

    <label>Role:</label>
    <select v-model="role">
      <!-- <option value=""></option> -->
      <option value="developer">Web Developer</option>
      <option value="backend developer">Backend Developer</option>
      <option value="designer">Web Designer</option>
    </select>

    <label>Skills:</label>
    <input @keyup="addSkill" type="text" v-model="tempSkill" />
    <div v-for="skill in skills" :key="skill" class="pill">
      <p>{{ skill }}</p>
      <span class="xbtn" @click="deleteSkill(skill)">X</span>
    </div>

    <div class="terms">
      <input v-model="terms" type="checkbox" required />
      <label>Accept Terms and Conditions</label>
    </div>
    <!-- <div>
      <input v-model="names" value="Mario" type="checkbox" />
      <label>Mario</label>
    </div>
    <div>
      <input v-model="names" value="Luigi" type="checkbox" />
      <label>Luigi</label>
    </div>
    <div>
      <input v-model="names" value="Yoshi" type="checkbox" />
      <label>Yoshi</label>
    </div> -->
    <div class="submit">
      <button>Submit</button>
    </div>
  </form>
</template>

<script>
export default {
  data() {
    return {
      email: "",
      password: "",
      role: "",
      terms: false,
      //   names: [],
      tempSkill: "",
      skills: [],
      passwordError: "",
    };
  },
  methods: {
    addSkill(e) {
      if (e.keyCode === 13 && this.tempSkill) {
        if (this.skills.includes(this.tempSkill)) {
          alert("Skill already listed");
        } else {
          this.skills.push(this.tempSkill);
          this.tempSkill = "";
        }
      } else if (e.key === "," && this.tempSkill) {
        this.tempSkill = this.tempSkill.slice(0, -1);
        if (this.skills.includes(this.tempSkill)) {
          alert("Skill already listed");
        } else {
          this.skills.push(this.tempSkill);
          this.tempSkill = "";
        }
      } else {
        return;
      }
    },
    deleteSkill(skill) {
      this.skills = this.skills.filter((item) => {
        return item !== skill;
      });
    },
    handleSubmit(e) {
      console.log("hello");
      this.passwordError =
        this.password.length > 5
          ? ""
          : "Password must be at least 6 characters long";
      if (!this.passwordError) {
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
  color: rgb(126, 126, 126);
  display: inline-block;
  margin: 25px 0 15px;
  font-size: 0.65rem;
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
.pill {
  display: inline-block;
  margin: 20px 10px 0 0;
  padding: 6px 12px 4px 12px;
  background: #eee;
  border-radius: 20px;
  font-size: 14px;
  letter-spacing: 1px;
  font-weight: bold;
  color: #777;
}
.pill .xbtn {
  display: inline-block;
  padding-left: 8px;
  margin: 0;
  font-size: 8px;
  border: none;
  align-items: center;
  color: red;
  cursor: pointer;
}
.pill p {
  display: inline-block;
  margin: 0;
}

button {
  background: rgb(128, 128, 255);
  border: 0;
  width: 100%;
  font-size: 16px;
  font-weight: bold;
  padding: 10px 20px;
  margin-top: 20px;
  color: white;
}
.error {
  color: #ff0062;
  margin-top: 10px;
  font-size: 0.8rem;
}

@media only screen and (max-width: 576px) {
  form {
    max-width: 75%;
  }
}
</style>

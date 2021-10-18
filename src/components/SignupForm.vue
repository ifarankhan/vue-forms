<template>
  <form>
    <label>Email:</label>
    <input type="email" required v-model="email" />

    <label>Password:</label>
    <input type="password" required v-model="pass" />

    <label>Role:</label>
    <select v-model="role">
      <option value="designer">Web designer</option>
      <option value="developer">Web developer</option>
    </select>

    <label>Skills</label>
    <input type="text" v-model="tempSkills" @keyup="addSkills" />
    <div class="skill-set">
      <div class="pill" v-for="(skill, index) in skills" :key="index">
        {{ skill }}
        <div class="cross" @click="deleteSkill($event,index)">x</div>  

      </div>
    </div>

    <div class="terms">
      <input type="checkbox" v-model="terms" required />
      <label>Accept terms and conditions</label>
    </div>
  </form>
  <p>
    Email : {{ email }}<br />
    Password: {{ pass }} <br />
    Roles: {{ role }} <br />
  </p>
</template>

<script>
export default {
  data() {
    return {
      email: "123",
      pass: "",
      role: "",
      terms: true,
      tempSkills: "",
      skills: [],
    };
  },
  methods: {
    addSkills(e) {
      if (e.key === "," && this.tempSkills !== "") {
        var skillRefined = "";
        var skillRefined = this.tempSkills.replace(/,/g, "");
        if (!this.skills.includes(skillRefined)) {
          this.skills.push(skillRefined);
        }
        this.tempSkills = "";
      }
    },
    deleteSkill(e,clickedskill){
        var removeSkill = this.skills[clickedskill];
        if(this.skills.indexOf(removeSkill) !== -1){

            this.skills.splice(clickedskill, 1);
        }
    }
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
</style>

<template>
  <li>
    <p>
      <span class="highlight">{{ note }}</span> Notunuza Verdiğiniz Önem
      Derecesi
      <span :class="onemDerecesi">{{ onemlilikDerecesi }}</span>
    </p>
  </li>
</template>

<script>
export default {
  props: ["note", "onemlilikDerecesi"],
  computed: {
    onemDerecesi() {
      return "highlight onemlilikDerecesi--" + this.onemlilikDerecesi;
    },
  },
};
</script>

<style scoped>
li {
  margin: 1rem 0;
  border: 1px solid #ccc;
  padding: 1rem;
}

h3,
p {
  font-size: 1rem;
  margin: 0.5rem 0;
}

.highlight {
  font-weight: bold;
}

.onemlilikDerecesi--1 {
  color: rgb(156, 201, 216);
}

.onemlilikDerecesi--2 {
  color: lightseagreen;
}

.onemlilikDerecesi--3 {
  color: steelblue;
}

.onemlilikDerecesi--4 {
  color: rgb(216, 136, 149);
}

.onemlilikDerecesi--5 {
  color: #ad0a0a;
}
</style>
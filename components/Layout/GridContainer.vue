<template>
  <div class="container grid">
    <slot></slot>
  </div>
</template>

<style>
.container {
  position: relative;
  padding: 15vh var(--spacing-5);
  justify-content: center;
  margin: 0 auto;
  background-color: var(--background-primary);
  z-index: 3;
}

.grid {
  display: grid;
  grid-template-columns: repeat(12, 1fr);
  column-gap: 1.3888888889vw;
  row-gap: 1.3888888889vw;
  overflow: hidden;
}

@media (max-width: 767px) {
  .container {
    padding: 3vh var(--spacing-4);
  }

  .grid,
  .grid.container {
    display: grid;
    grid-template-columns: repeat(6, 1fr);
    column-gap: 2.3333333333vw;
  }
}
</style>

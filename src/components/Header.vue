<template>
    <nav class="navbar navbar-expand-lg bg-light">
  <div class="container-fluid">
    <div class="collapse navbar-collapse" id="navbarText">
      <ul class="navbar-nav mr-auto mb-2 mb-lg-0">
        <li class="nav-item">
          <a class="nav-link disabled" href="#">Quiz</a>
        </li>
        <li class="nav-item">
          <a class="nav-link disabled" href="#">{{this.correctNum}} of {{this.questionNum}}</a>
        </li>
      </ul>
    </div>
  </div>
</nav>
</template>
<script>
export default {
  name: 'Header',
  props: {
    questionNum: Number,
    correctNum: Number
  }
  
}

  </script>
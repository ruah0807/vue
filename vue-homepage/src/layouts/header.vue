<template>
<nav class="navbar navbar-expand-lg navbar-dark bg-dark">
<div class="container-fluid">
<a class="navbar-brand" href="#">SOLD OUT</a>
<button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarSupportedContent" aria-controls="navbarSupportedContent" aria-expanded="false" aria-label="Toggle navigation">
<span class="navbar-toggler-icon"></span>
</button>
<div class="collapse navbar-collapse" id="navbarSupportedContent">
<ul class="navbar-nav me-auto mb-2 mb-lg-0">
<li class="nav-item">
<router-link class="nav-link" to="/">홈</router-link>
</li>
<li class="nav-item">
<router-link class="nav-link" to="/">제품리스트</router-link>
</li>
<li class="nav-item">
<router-link class="nav-link" to="/detail">제품상세페이지</router-link>
</li>
<li class="nav-item">
<router-link class="nav-link" to="/create">제품등록페이지</router-link>
</li>
</ul>
<form class="d-flex">
<input class="form-control me-2" type="search" placeholder="Search" aria-label="Search">
<button class="btn btn-outline-success" type="submit">Search</button>
</form>
</div>
</div>
</nav>
</template>
<script>
// eslint-disable-next-line
/* eslint-disable */
export default {
	name: 'header'
}
</script>

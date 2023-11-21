<template>
  <nav class="navbar navbar-expand-lg navbar-light bg-light p-3">
    <NuxtLink class="navbar-brand" to="/">Home</NuxtLink>
    <button
      class="navbar-toggler"
      type="button"
      data-toggle="collapse"
      data-target="#navbarNavAltMarkup"
      aria-controls="navbarNavAltMarkup"
      aria-expanded="false"
      aria-label="Toggle navigation"
    >
      <span class="navbar-toggler-icon"></span>
    </button>

    <div class="collapse navbar-collapse" id="navbarNavAltMarkup">
      <div class="navbar-nav">
        <NuxtLink class="nav-item nav-link active" href="/"
          >Home <span class="sr-only">(current)</span></NuxtLink
        >
        <NuxtLink class="nav-item nav-link" href="/add">Add</NuxtLink>
        <NuxtLink class="nav-item nav-link" href="/all">All</NuxtLink>
        <NuxtLink class="nav-item nav-link" href="/addImg">Add-Img</NuxtLink>
      </div>
    </div>
  </nav>
  <div class="container">
    <NuxtPage class="pt-4" />
  </div>
</template>

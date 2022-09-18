<!-- this component can hold site navigation -->
<!-- if we put it here we can avoid having to repeat the code -->
<template>
	<nav>

    <NuxtLink to="/">
          <img src="~assets/images/cmlogonav.png" alt="" class="logonav"></img>
      </NuxtLink>

      <NuxtLink to="/">
          <button type="button" class="btn btn-primary">
            Home
          </button>
      </NuxtLink>

    <NuxtLink to="/about">
      <button type="button" class="btn btn-primary">
            About
          </button>
    </NuxtLink>

		<NuxtLink to="/buildings">
      <button type="button" class="btn btn-primary">
            Buildings
          </button>
    </NuxtLink>
    
    <NuxtLink to="/partners">
      <button type="button" class="btn btn-primary">
            Partners
          </button>
    </NuxtLink>

    <NuxtLink to="/events">
      <button type="button" class="btn btn-primary">
            Events
          </button>
    </NuxtLink>

    <NuxtLink to="/links">
      <button type="button" class="btn btn-primary">
            Links
          </button>
    </NuxtLink>

    <NuxtLink to="/videos">
      <button type="button" class="btn btn-primary">
            Videos
          </button>
    </NuxtLink>
          




	</nav>
</template>

<!-- sets the colour of EVERY TEXT LINK (not including nav bar) -->
<style> 
  nav, a {
    color: #2e2e2e;
  }
</style>

<style scoped>
  @import url('http://fonts.cdnfonts.com/css/futura-std-4');
</style>


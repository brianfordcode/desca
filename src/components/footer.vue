<template>
<!-- TODO: KEEP FOOTER AT BOTTOM ALWAYS -->
    <div class="container">

        <div class="wrapper">

            <div class="page-links-wrapper">
                <router-link to="/">Home</router-link>
                <router-link to="/">About</router-link>
                <router-link to="/">Contact</router-link>
                <router-link to="/">Blog</router-link>
                <router-link to="/">FAQ</router-link>
            </div>

            <div class="logo-links-wrapper">
                <img
                    id="logo"
                    src="/desca-logo.png"
                    alt="desca-logo"
                    @click="$router.push('/')"
                />

               <div class="social-links">
                    <a href="https://www.twitch.tv" target="_blank">
                        <img
                            class="sm-logo"
                            src="/social-links/twitch-logo.png"
                            alt="twitch"
                        />
                    </a>
                    <a href="https://www.facebook.com" target="_blank">
                        <img
                            class="sm-logo"
                            src="/social-links/facebook-logo.png"
                            alt="twitch"
                        />
                    </a>
                    <a href="https://www.discord.com" target="_blank">
                        <img
                            class="sm-logo"
                            src="/social-links/discord-logo.png"
                            alt="twitch"
                        />
                    </a>
               </div> 

            </div>

        </div>

    </div>

</template>

<script>
export default {

}
</script>

<style scoped>

.container {
    height: min-content;
    padding: 20px;
    /* width: 100vw; */
    background: rgb(13, 13, 118);
    /* bottom: 0; */
    box-shadow: 0px 0px 33px -20px #000000;
}

.wrapper {
    max-width: 1200px;
    /* border: 1px solid; */
    margin: 0 auto;
    display: flex;
    justify-content: space-between;
}

.page-links-wrapper {
    display: grid;
    /* border: 1px solid; */
    width: 150px;
    grid-template-columns: 1fr 1fr;
}

a {
    color: white;
    text-decoration: none;
}

#logo {
    width: 100px;
}

.social-links > *:not(:last-child) {
    margin-right: 5px;
}

.sm-logo {
    width: 20px;
}


</style>
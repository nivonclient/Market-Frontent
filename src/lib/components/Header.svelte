<script lang="ts">
    import { auth } from "$lib/auth";
	import Button from './Button.svelte';
</script>

<div class="header layout" id="nav">
    <div class="left-side">
        <div class="wrapper-2c">
            <div class="logo"></div>
            <span class="title">Pumpkin Market</span>
        </div>
    </div>
    <!-- <div class="center">
        <a href="#" class="btn"><i class="fa-solid fa-magnifying-glass"></i>Browse</a>
    </div> -->
    <div class="right-side">
        {#if auth.isLoggedIn}
            <div class="btn-group-row">
                <Button href="/" color="orange">Publish</Button>
                <Button href="/" color="skin">Account</Button>
            </div>
        {:else}
            <div class="btn-group-row">
                <Button href="/" color="orange"><i class="fa-solid fa-right-to-bracket"></i>Login</Button>
                <Button href="/" color="skin"><i class="fa-solid fa-user-plus"></i>Signup</Button>
            </div>
        {/if}
    </div>
</div>

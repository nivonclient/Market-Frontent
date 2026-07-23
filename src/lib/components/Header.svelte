<script lang="ts">
    import { isLogged } from '$lib/auth/auth';
</script>

<div class="header layout" id="nav">
    <div class="left-side">
        <span class="title">Pumpkin Market</span>
    </div>
    <!-- <div class="center">
        <a href="#" class="btn"><i class="fa-solid fa-magnifying-glass"></i>Browse</a>
    </div> -->
    <div class="right-side">
        {#if isLogged}
            <div class="btn-group-row">
                <a href="#" class="btn orange">Publish</a>
                <a href="#" class="btn skin">Account</a>
            </div>
        {:else}
            <a href="#" class="btn">Login</a>
            <a href="#" class="btn">Signup</a>
        {/if}
    </div>
</div>

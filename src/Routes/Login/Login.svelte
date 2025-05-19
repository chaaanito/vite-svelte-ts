<script lang="ts">
    import { toast } from "svelte-sonner";
    import { pb } from "../../lib/Pocketbase.svelte";
    import { fade } from "svelte/transition";

    let username = $state('')
    let password = $state('')

    const login = (e: SubmitEvent) => {
        e.preventDefault()
        toast.promise(pb.collection('0_STUDENT').authWithPassword(username,password),{
            loading: "Logging in...",
            success: `Welcome ${username}!`,
            error: (data: any) => {
                return `${data.data.status} : ${data.message}`
            }
        })
    }
    
</script>


<!-- svelte-ignore a11y_label_has_associated_control -->
<form onsubmit={login} class="w-full" in:fade out:fade>
    <fieldset class="fieldset bg-base-200 border-base-300 rounded-box w-xs border p-4 mx-auto mt-[20%]">
        <legend class="fieldset-legend">Login</legend>
      
        <label class="label">Username</label>
        <input type="text" class="input validator" placeholder="Username" bind:value={username} required/>
      
        <label class="label">Password</label>
        <input type="password" class="input validator" placeholder="Password" bind:value={password} required/>
      
        <button class="btn btn-success mt-4" type="submit">Login</button>
      </fieldset>
</form>
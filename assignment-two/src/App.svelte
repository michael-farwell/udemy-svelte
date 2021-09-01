<script>
    let userPassword = "";
    let passwordValidity = "valid";
    let savedPasswords = [];

    function removePassword(password) {
        savedPasswords = savedPasswords.filter((pwd) => pwd !== password);
    }

    function savePassword() {
        savedPasswords = [...savedPasswords, userPassword.trim()];
        userPassword = "";
    }

    $: if (!userPassword.trim().length) {
        passwordValidity = "no password";
    } else if (userPassword.trim().length < 5) {
        passwordValidity = "too short";
    } else if (userPassword.trim().length > 10) {
        passwordValidity = "too long";
    } else {
        passwordValidity = "valid";
    }
</script>

<main>
    <h1>Assignment</h1>

    <p>Solve these tasks.</p>

    <ol>
        <li>
            Add a password input field and save the user input in a variable.
        </li>
        <li>
            Output "Too short" if the password is shorter than 5 characters and
            "Too long" if it's longer than 10.
        </li>
        <li>
            Output the password in a paragraph tag if it's between these
            boundaries.
        </li>
        <li>Add a button and let the user add the passwords to an array.</li>
        <li>
            Output the array values (= passwords) in a unordered list (ul tag).
        </li>
        <li>Bonus: If a password is clicked, remove it from the list.</li>
    </ol>

    <hr />

    <input type="password" bind:value={userPassword} />

    <button on:click={savePassword} disabled={passwordValidity !== "valid"}>
        Save Password
    </button>

    <div>
        {#if passwordValidity === "too short"}
            <p class="error__text">Too short</p>
        {:else if passwordValidity === "too long"}
            <p class="error__text">Too long</p>
        {:else if passwordValidity === "no password"}
            <p class="error__text">Please enter a password</p>
        {:else}
            <p class="success__text">{userPassword}</p>
        {/if}
    </div>

    <h2>Saved Passwords</h2>
    <ul>
        {#each savedPasswords as password (password)}
            <li on:click={removePassword(password)}>{password}</li>
        {/each}
    </ul>
</main>

<style>
    .error__text {
        color: red;
    }

    .success__text {
        color: green;
    }

    li:hover {
        cursor: pointer;
    }
</style>

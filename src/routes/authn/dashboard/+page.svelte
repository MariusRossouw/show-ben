<script>
  import { getLS } from "@stratech-team/svelte-component-library";
  import { onMount } from "svelte";

  let session = {};

  onMount(() => {
    getSessionID();
  });

  function getSessionID() {
    session = getLS(import.meta.env.VITE_APP_NAME + "-user-login-response");
    readDashboard();
  }

  function readDashboard() {
    let request = {
      session_id: session.data.session_id,
    };
    fetch("dashboard", {
      body: request,
    }).then((res) => {
      console.info("dashboard response: ", res);
    });
  }
</script>

<div class="desktop-content-container">
  <!-- Content goes here -->
  <h2>Dashboard</h2>
</div>

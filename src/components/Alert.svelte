<script lang="ts">
    export let err: Error;
</script>

<div class="container animate__animated animate__headShake alert alert-danger alert" role="alert">
    {err}
 </div>

 <style>
     .alert {
         margin-top: 30px;
         width: 70%;
     }
 </style>
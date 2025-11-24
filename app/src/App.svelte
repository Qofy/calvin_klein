<script>
  import Navogation from "./component/Navogation.svelte";
  import MainSide from "./pages/Main&Side.svelte";


</script>

<main>
  <Navogation/>
  <MainSide/>
</main>

<style>
  :global(body){
        height: 100vw;
    }
  main{
    display: flex;
    flex-direction: column;
    width: 100%;
    /* background-color: aqua;  */
    gap: 10rem;
    height: 100%;
  }
</style>
<script>
import "../component/style.css"
</script>

<nav>
<div>left</div>
<div>middle</div>
<div>right</div>
</nav>

<style>
    
    nav{
        position: fixed;
        top: 0;
        display: flex;
        justify-content: space-between;
        width: 100%;
        padding: 0 2rem;
        /* background-color: aqua; */
        align-items: center;
        height: clamp(50px, 70vw, 65px);
    }
</style>
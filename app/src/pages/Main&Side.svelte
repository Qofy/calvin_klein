<script>

</script>

<main>
<div class="side-main">
    <div class="hero">
        <div></div>
        <div></div>
        <div></div>
        <div></div>
    </div>
    <div class="sidebar"></div>
</div>
<div >shdgsh</div>
</main>

<style>
    main{
        margin-top: 5rem;
    height: clamp(40%, 70vw, 60%);
    /* background-color: black; */

    }
.side-main{
    display: flex;
    height: clamp(40%, 100%, 60%);
    width: 100%;
}

.sidebar{
background-color: yellow;
width: 30%;
height: 100%;

}

.hero{
background-color: blue;
width: 70%;
height: 100%;
display: grid;
grid-template-columns: repeat(auto-fit, minmax(min(300px,100%),1fr));
}
</style>
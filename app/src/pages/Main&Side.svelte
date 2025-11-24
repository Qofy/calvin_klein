<script>
import bk1 from "../../public/assets/bike/b1.png"
import bk2 from "../../public/assets/bike/b2.png"
import bk3 from "../../public/assets/bike/b3.png"
import bk4 from "../../public/assets/bike/b4.png"
</script>

<main>
<div class="side-main">
    <div class="hero">
        <div style="background-image: url({bk1});"></div>
        <div style="background-image: url({bk2});"></div>
        <div style="background-image: url({bk3});"></div>
        <div style="background-image: url({bk4});"></div>
    </div>
    <div class="sidebar"></div>
</div>
<div >shdgsh</div>
</main>

<style>
    main{
        margin-top: 5rem;
    height: clamp(40%, 100vw, 100%);
    /* background-color: black;  */

    }
.side-main{
    display: flex;
    height: clamp(40%, 100%, 60%);
    width: 100%;
}

.sidebar{
background-color: yellow;
width: 30%;
 height: clamp(40%, 100vw, 80.7rem);



}

.hero{
 /* background-color: blue; */
width: 70%;
 height: clamp(40%, 100vw, 80.7rem);
display: grid;
grid-template-columns: repeat(2, minmax(min(300px,100%),1fr));
gap: .6rem;
/* overflow-y: scroll;
scrollbar-width: none; */

}

.hero div{
    background-position: center;
    background-repeat: no-repeat;
    background-size:cover;
    height: 40rem;
}
</style>
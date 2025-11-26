<script>
  import {Search, Globe, Heart, UserRound, ShoppingBag} from "lucide-svelte";
  import ProductDetails from "./pages/ProductDeatils.svelte";
  import Carousel from "./pages/Carousel.svelte";
  import Footer from "./pages/Footer.svelte";
  
  
  import data from '../public/data/article.json';
  
  const { navigation, product, carousel, footer,site } = data;
</script>

<main>
  <nav>
    <div class="nav">
      {#each navigation.mainLinks as link}
        <a href={link.href}>{link.label}</a>
      {/each}
    </div>
    
    <div>
     <img class="logo" src={site.logo} alt="logo"> 
    </div>
    
    <div class="icon">
      <a href="#"><Search/></a>
      <a href="#"><Globe/></a>
      <a href="#"><Heart/></a>
      <a href="#"><UserRound/></a>
      <a href="#"><ShoppingBag/></a>
    </div>
  </nav>
  
  <div class="hero">
    {#each product.hero.images as image}
      <div style="background-image: url({image});"></div>
    {/each}
  </div>

  <div class="sidebar">
    <ProductDetails data={product} />
  </div>

  <div class="carousel">
    <div class="carousel-section">
      <Carousel data={carousel} />
    </div>
  </div>
  
  <footer class="footer">
    <Footer data={footer} />
  </footer>
</main>

<style>
  :global(body){
    height: 100vh;
    margin: 0;
  }
 
  main{
    display: grid;
    grid-template-columns: repeat(5, 1fr);
    grid-template-rows: 65px repeat(9, 1fr);
    min-height: 100vh;
  }
  
  nav{
    grid-column: 1 / 6;
    grid-row: 1;
    position: fixed;
    top: 0;
    display: flex;
    justify-content: space-between;
    width: 100%;
    padding: 0 2rem;
    align-items: center;
    height: 65px;
    z-index: 1000;
    box-sizing: border-box;
    background-image: linear-gradient(to bottom right, #e1d7bd, #e5dcc6, #efeade);
    color: #ce2f24;
  }

  .nav{
    display: flex;
    list-style: none;
    gap: clamp(.8rem, 2vw, 1.5rem);
    align-items: center;
  }

  .icon{
    display: flex;
    gap: clamp(.8rem, 2vw, 1.5rem);
    align-items: center;
  }

  .hero{
    /* background-color: blue; */
    grid-column: 1 / 4;
    grid-row: 2 / 7;
    grid-template-columns: repeat(2, minmax(min(300px,100%),1fr));
    /* background-color: #d32f2f; */
  }

  .hero div{
    background-position: center;
    background-repeat: no-repeat;
    background-size:cover;
    height: 45rem;
}

.logo{
  width: 150px;
}

  /**----------------Sidebar -------------------------*/
  .sidebar{
    /* background-color: burlywood; */
    grid-column: 4 / 6;
    grid-row: 2 / 7;
    display: flex;
    flex-direction: column;
    padding: 5rem 2rem;
    /* background-color: rgb(161, 200, 234); */
  }
  
  
/*----------------Carousel-----------------*/
  .carousel{
    /* background-color: cadetblue; */
    grid-column: 1 / 6;
    grid-row: 6/ 8;
  }

  .footer{
    /* background-color: brown; */
    grid-row: 8/ 11;
    grid-column: 1 / 6;
     background-color: #fbb900;
    color: #e43417;
    padding: 0;
    text-align: center;
    padding: 4rem 2rem;
    border-bottom: 1px solid #333;
  }
</style>
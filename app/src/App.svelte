<script>
  import {Search, Globe, Heart, UserRound, ShoppingBag, X} from "lucide-svelte";
  import ProductDetails from "./pages/ProductDeatils.svelte";
  import Carousel from "./pages/Carousel.svelte";
  import Footer from "./pages/Footer.svelte";
  
  
  import data from '../public/data/article.json';
  
  const { navigation, product, carousel, footer,site } = data;

 
  let isOpen = false;
  let wishlist = [];
  let isWishlistOpen = false;
  
  function toggleCart() {
    isOpen = !isOpen;
  }
  
   function toggleWishlist() {
    isWishlistOpen = !isWishlistOpen;
  }
  
  function closeMenu() {
    isOpen = false;
  }
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
      <a href="#" on:click={toggleWishlist} class="wishlist-icon">
        <Heart fill={wishlist.length > 0 ? '#ce2f24' : 'none'} color={wishlist.length > 0 ? '#ce2f24' : 'currentColor'} />
        {#if wishlist.length > 0}
          <span class="badge">{wishlist.length}</span>
        {/if}
      </a>
      <a href="#"><UserRound/></a>
      <a href="#" on:click={toggleCart}><ShoppingBag/></a>
    </div>
  </nav>
  
<!----------------Shopping Cart Overlay---------------------------->

  {#if isOpen}
    <div class="cart-overlay" on:click={closeMenu}></div>
    <div class="cart-slider">
      <div class="cart-header">
        <h2>Warenkorb</h2>
        <button class="close-btn" on:click={closeMenu} aria-label="Close cart">
          <X />
        </button>
      </div>
      
      <div class="cart-content">
        <!-- Sample cart items - replace with your actual cart data -->
        <div class="cart-item">
          <img src="/path/to/product-image.jpg" alt="Product" />
          <div class="item-details">
            <h3>Product Name</h3>
            <p class="item-price">€99.99</p>
            <div class="item-quantity">
              <button>-</button>
              <span>1</span>
              <button>+</button>
            </div>
          </div>
        </div>
        
        <div class="cart-item">
          <img src="/path/to/product-image.jpg" alt="Product" />
          <div class="item-details">
            <h3>Another Product</h3>
            <p class="item-price">€149.99</p>
            <div class="item-quantity">
              <button>-</button>
              <span>2</span>
              <button>+</button>
            </div>
          </div>
        </div>
        
        <!-- Empty cart message -->
        <!-- <div class="empty-cart">
          <ShoppingBag />
          <p>Ihr Warenkorb ist leer</p>
        </div> -->
      </div>
      
      <div class="cart-footer">
        <div class="cart-total">
          <span>Gesamt:</span>
          <span class="total-price">€399.97</span>
        </div>
        <button class="checkout-btn">Zur Kasse</button>
      </div>
    </div>
  {/if}

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
      <Carousel 
        data={carousel} 
        bind:wishlist={wishlist}
        bind:isWishlistOpen={isWishlistOpen}
      />
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
    margin: 0;
    padding: 0;
  }

  .nav a {
    text-decoration: none;
    color: inherit;
    transition: opacity 0.2s;
  }

  .nav a:hover {
    opacity: 0.7;
  }

  .icon{
    display: flex;
    gap: clamp(.8rem, 2vw, 1.5rem);
    align-items: center;
  }

  .icon a {
    display: flex;
    align-items: center;
    color: inherit;
    cursor: pointer;
    position: relative;
    transition: all 0.2s;
  }

  .icon a:hover {
    opacity: 0.7;
    transform: scale(1.05);
  }

  .wishlist-icon {
    position: relative;
  }

  .badge {
    position: absolute;
    top: -8px;
    right: -8px;
    background: #ce2f24;
    color: white;
    border-radius: 50%;
    min-width: 18px;
    height: 18px;
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 11px;
    font-weight: 600;
    padding: 2px;
  }

  /**-----------------shopping cart-------------------------*/
.cart-overlay {
    position: fixed;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    background: rgba(0, 0, 0, 0.5);
    z-index: 1001;
    animation: fadeIn 0.3s ease;
  }

  .cart-slider {
    position: fixed;
    top: 0;
    right: 0;
    width: clamp(320px, 90vw, 450px);
    height: 100vh;
    background: #fff;
    z-index: 1002;
    display: flex;
    flex-direction: column;
    box-shadow: -4px 0 20px rgba(0, 0, 0, 0.15);
    animation: slideIn 0.3s ease;
  }

  .cart-header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 1.5rem 2rem;
    background-image: linear-gradient(to bottom right, #e1d7bd, #e5dcc6, #efeade);
    border-bottom: 1px solid rgba(206, 47, 36, 0.2);
  }

  .cart-header h2 {
    margin: 0;
    color: #ce2f24;
    font-size: clamp(1.25rem, 3vw, 1.5rem);
    font-weight: 600;
  }

  .close-btn {
    background: none;
    border: none;
    color: #ce2f24;
    cursor: pointer;
    padding: 0.5rem;
    display: flex;
    align-items: center;
    justify-content: center;
    transition: all 0.2s;
    border-radius: 4px;
  }

  .close-btn:hover {
    background: rgba(206, 47, 36, 0.1);
    transform: rotate(90deg);
  }

  .close-btn :global(svg) {
    width: 24px;
    height: 24px;
  }

  .cart-content {
    flex: 1;
    overflow-y: auto;
    padding: 1.5rem;
    scrollbar-width: thin;
    scrollbar-color: #ce2f24 #f3f6fb;
  }

  .cart-content::-webkit-scrollbar {
    width: 6px;
  }

  .cart-content::-webkit-scrollbar-track {
    background: #f3f6fb;
  }

  .cart-content::-webkit-scrollbar-thumb {
    background: #ce2f24;
    border-radius: 3px;
  }

  .cart-item {
    display: flex;
    gap: 1rem;
    padding: 1rem;
    border-bottom: 1px solid #eee;
    transition: background-color 0.2s;
  }

  .cart-item:hover {
    background-color: #fafafa;
  }

  .cart-item img {
    width: 80px;
    height: 80px;
    object-fit: cover;
    border-radius: 8px;
    background: #f0f0f0;
  }

  .item-details {
    flex: 1;
    display: flex;
    flex-direction: column;
    gap: 0.5rem;
  }

  .item-details h3 {
    margin: 0;
    font-size: 1rem;
    font-weight: 600;
    color: #333;
  }

  .item-price {
    margin: 0;
    color: #ce2f24;
    font-weight: 600;
    font-size: 1.1rem;
  }

  .item-quantity {
    display: flex;
    align-items: center;
    gap: 0.75rem;
  }

  .item-quantity button {
    background: #f0f0f0;
    border: none;
    width: 28px;
    height: 28px;
    border-radius: 4px;
    cursor: pointer;
    display: flex;
    align-items: center;
    justify-content: center;
    font-weight: 600;
    transition: all 0.2s;
  }

  .item-quantity button:hover {
    background: #ce2f24;
    color: #fff;
  }

  .item-quantity span {
    min-width: 30px;
    text-align: center;
    font-weight: 600;
  }

  .empty-cart {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    height: 100%;
    color: #999;
    gap: 1rem;
  }

  .empty-cart :global(svg) {
    width: 64px;
    height: 64px;
    opacity: 0.3;
  }

  .cart-footer {
    padding: 1.5rem 2rem;
    border-top: 2px solid #eee;
    background: #fafafa;
  }

  .cart-total {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-bottom: 1rem;
    font-size: 1.1rem;
  }

  .total-price {
    font-size: 1.5rem;
    font-weight: 700;
    color: #ce2f24;
  }

  .checkout-btn {
    width: 100%;
    padding: 1rem;
    background: #ce2f24;
    color: #fff;
    border: none;
    border-radius: 8px;
    font-size: 1rem;
    font-weight: 600;
    cursor: pointer;
    transition: all 0.3s;
  }

  .checkout-btn:hover {
    background: #a52419;
    transform: translateY(-2px);
    box-shadow: 0 4px 12px rgba(206, 47, 36, 0.3);
  }

  .checkout-btn:active {
    transform: translateY(0);
  }

  /* ============================================
     ANIMATIONS
     ============================================ */
  @keyframes fadeIn {
    from {
      opacity: 0;
    }
    to {
      opacity: 1;
    }
  }

  @keyframes slideIn {
    from {
      transform: translateX(100%);
    }
    to {
      transform: translateX(0);
    }
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
  width: 230px;
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
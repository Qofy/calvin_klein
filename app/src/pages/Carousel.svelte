<script>
  import { Heart, ChevronRight } from "lucide-svelte";
  
  export let data;
  
  const { title, products } = data;

  let scrollContainer;
  
  function scrollRight() {
    if (scrollContainer) {
      scrollContainer.scrollBy({ left: 300, behavior: 'smooth' });
    }
  }
</script>

<div class="carousel-section">
  <h2>{title}</h2>
  
  <div class="carousel-wrapper">
    <div class="carousel-container" bind:this={scrollContainer}>
      {#each products as product}
        <div class="product-card">
          <div class="product-image">
            <button class="favorite-btn">
              <Heart size={20} />
            </button>
            {#if product.discount}
              <div class="discount-badge">{product.discount}</div>
            {/if}
            <img src={product.image} alt={product.title} />
          </div>
          
          <div class="product-info">
            <h3 class="product-title">{product.title}</h3>
            <div class="product-price">
              <span class="original-price">{product.originalPrice}</span>
              {#if product.salePrice !== product.originalPrice}
                <span class="sale-price">{product.salePrice}</span>
              {/if}
            </div>
          </div>
          
          <div class="product-actions">
            <select class="size-select">
              <option>Größe</option>
              <option>XS</option>
              <option>S</option>
              <option>M</option>
              <option>L</option>
              <option>XL</option>
            </select>
            
            <button class="add-to-cart">Hinzufügen</button>
          </div>
        </div>
      {/each}
    </div>
    
    <button class="scroll-btn" on:click={scrollRight}>
      <ChevronRight size={24} />
    </button>
  </div>
</div>


<style>
  .carousel-section {
    padding: 3rem 2rem;
    background-color: #fff;
  }

  h2 {
    font-size: 1.25rem;
    font-weight: 600;
    margin-bottom: 2rem;
    letter-spacing: 0.5px;
    color: #ce2f24;
  }

  .carousel-wrapper {
    position: relative;
  }

  .carousel-container {
    display: flex;
    gap: 1rem;
    overflow-x: auto;
    scroll-behavior: smooth;
    padding-bottom: 1rem;
    scrollbar-width: none;
  }

  .carousel-container::-webkit-scrollbar {
    display: none;
  }

  .product-card {
    min-width: 240px;
    flex-shrink: 0;
    display: flex;
    flex-direction: column;
  }

  .product-image {
    position: relative;
    background-color: #f5f5f5;
    aspect-ratio: 3/4;
    overflow: hidden;
    margin-bottom: 0.75rem;
  }

  .product-image img {
    width: 100%;
    height: 100%;
    object-fit: cover;
  }

  .favorite-btn {
    position: absolute;
    top: 1rem;
    right: 1rem;
    background: white;
    border: none;
    width: 36px;
    height: 36px;
    border-radius: 50%;
    display: flex;
    align-items: center;
    justify-content: center;
    cursor: pointer;
    z-index: 10;
    transition: all 0.2s;
  }

  .favorite-btn:hover {
    transform: scale(1.1);
  }

  .discount-badge {
    position: absolute;
    bottom: 1rem;
    left: 0;
    background-color: #d32f2f;
    color: white;
    padding: 0.25rem 0.75rem;
    font-size: 0.875rem;
    font-weight: 600;
  }

  .product-info {
    margin-bottom: 1rem;
  }

  .product-title {
    font-size: 0.875rem;
    font-weight: 400;
    margin-bottom: 0.5rem;
    color: #1a1919;
    white-space: nowrap;
    overflow: hidden;
    text-overflow: ellipsis;
  }

  .product-price {
    display: flex;
    align-items: center;
    gap: 0.5rem;
    font-size: 0.875rem;
  }

  .original-price {
    color: #1a1919;
    font-weight: 600;
  }

  .sale-price {
    color: #d32f2f;
    font-weight: 600;
  }

  .product-actions {
    display: flex;
    flex-direction: column;
    gap: 0.75rem;
    margin-top: auto;
  }

  .size-select {
    width: 100%;
    padding: 0.75rem 1rem;
    border: 1px solid #ddd;
    background-color: white;
    font-size: 0.875rem;
    cursor: pointer;
    appearance: none;
    background-image: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='12' height='12' viewBox='0 0 12 12'%3E%3Cpath fill='%23333' d='M6 9L1 4h10z'/%3E%3C/svg%3E");
    background-repeat: no-repeat;
    background-position: right 1rem center;
    padding-right: 2.5rem;
  }

  .size-select:hover {
    border-color: #999;
  }

  .add-to-cart {
    width: 100%;
    padding: 0.75rem 1rem;
    background-color: #ce2f24;
    color: white;
    border: none;
    font-size: 0.875rem;
    font-weight: 500;
    cursor: pointer;
    transition: background-color 0.2s;
  }

  .add-to-cart:hover {
    background-color: #333;
  }

  .scroll-btn {
    position: absolute;
    right: 0;
    top: 50%;
    transform: translateY(-50%);
    background: white;
    border: 1px solid #ddd;
    width: 48px;
    height: 48px;
    border-radius: 50%;
    display: flex;
    align-items: center;
    justify-content: center;
    cursor: pointer;
    box-shadow: 0 2px 8px rgba(0,0,0,0.1);
    z-index: 10;
    transition: all 0.2s;
  }

  .scroll-btn:hover {
    background-color: #f5f5f5;
    box-shadow: 0 4px 12px rgba(0,0,0,0.15);
  }

  @media (max-width: 768px) {
    .scroll-btn {
      display: none;
    }
    
    .product-card {
      min-width: 180px;
    }
  }
</style>
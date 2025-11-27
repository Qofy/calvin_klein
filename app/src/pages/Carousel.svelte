<script>
  import { Heart, ChevronRight, X } from "lucide-svelte";
  
  export let data;
  export let wishlist = [];
  export let isWishlistOpen = false;
  export let cart = [];
  export let isCartOpen = false;
  
  const { title, products } = data;

  let scrollContainer;
  let selectedSizes = {}; // Track selected size for each product
  
  function scrollRight() {
    if (scrollContainer) {
      scrollContainer.scrollBy({ left: 300, behavior: 'smooth' });
    }
  }
  
  // Wishlist functions
  function toggleWishlist(product) {
    const index = wishlist.findIndex(item => item.id === product.id);
    
    if (index > -1) {
      wishlist = wishlist.filter(item => item.id !== product.id);
    } else {
      wishlist = [...wishlist, product];
    }
  }
  
  function isInWishlist(productId) {
    return wishlist.some(item => item.id === productId);
  }
  
  function removeFromWishlist(productId) {
    wishlist = wishlist.filter(item => item.id !== productId);
  }
  
  function closeWishlist() {
    isWishlistOpen = false;
  }
  
  // Cart functions
  function addToCart(product) {
    const size = selectedSizes[product.id];
    
    if (!size || size === 'Größe') {
      alert('Bitte wählen Sie eine Größe aus');
      return;
    }
    
    const existingItemIndex = cart.findIndex(
      item => item.id === product.id && item.size === size
    );
    
    if (existingItemIndex > -1) {
      // Increase quantity if item already exists
      cart[existingItemIndex].quantity += 1;
      cart = [...cart];
    } else {
      // Add new item
      cart = [...cart, {
        ...product,
        size: size,
        quantity: 1
      }];
    }
    
    // Reset selected size
    selectedSizes[product.id] = 'Größe';
    
    // Show success feedback
    const button = document.querySelector(`[data-product-id="${product.id}"] .add-to-cart`);
    if (button) {
      const originalText = button.textContent;
      button.textContent = 'Hinzugefügt!';
      button.style.background = '#4caf50';
      setTimeout(() => {
        button.textContent = originalText;
        button.style.background = '';
      }, 1000);
    }
  }
  
  function handleSizeChange(productId, event) {
    selectedSizes[productId] = event.target.value;
  }
</script>

<!-- Wishlist Slider -->
{#if isWishlistOpen}
  <div class="wishlist-overlay" on:click={closeWishlist}></div>
  <div class="wishlist-slider">
    <div class="wishlist-header">
      <h2>Wunschliste</h2>
      <button class="close-btn" on:click={closeWishlist} aria-label="Close wishlist">
        <X />
      </button>
    </div>
    
    <div class="wishlist-content">
      {#if wishlist.length === 0}
        <div class="empty-wishlist">
          <Heart size={64} />
          <p>Ihre Wunschliste ist leer</p>
          <small>Fügen Sie Produkte hinzu, indem Sie auf das Herz klicken</small>
        </div>
      {:else}
        {#each wishlist as product}
          <div class="wishlist-item">
            <img src={product.image} alt={product.title} />
            <div class="item-details">
              <h3>{product.title}</h3>
              <div class="item-price">
                <span class="price">{product.salePrice || product.originalPrice}</span>
                {#if product.salePrice !== product.originalPrice}
                  <span class="original">{product.originalPrice}</span>
                {/if}
              </div>
              <button class="remove-btn" on:click={() => removeFromWishlist(product.id)}>
                Entfernen
              </button>
            </div>
          </div>
        {/each}
      {/if}
    </div>
    
    {#if wishlist.length > 0}
      <div class="wishlist-footer">
        <p class="item-count">{wishlist.length} {wishlist.length === 1 ? 'Artikel' : 'Artikel'}</p>
        <button class="continue-btn">Alle zur Tasche hinzufügen</button>
      </div>
    {/if}
  </div>
{/if}

<div class="carousel-section">
  <h2>{title}</h2>
  
  <div class="carousel-wrapper">
    <div class="carousel-container" bind:this={scrollContainer}>
      {#each products as product}
        <div class="product-card" data-product-id={product.id}>
          <div class="product-image">
            <button 
              class="favorite-btn" 
              class:active={isInWishlist(product.id)}
              on:click={() => toggleWishlist(product)}
            >
              <Heart 
                size={20} 
                fill={isInWishlist(product.id) ? '#ce2f24' : 'none'}
                color={isInWishlist(product.id) ? '#ce2f24' : 'currentColor'}
              />
            </button>
            {#if product.discount}
              <div class="discount-badge">{product.discount}</div>
            {/if}
            <div class="discount-badge-img">
              <img src={product.image} alt={product.title} />
            </div>
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
            <select 
              class="size-select"
              value={selectedSizes[product.id] || 'Größe'}
              on:change={(e) => handleSizeChange(product.id, e)}
            >
              <option>Größe</option>
              <option>XS</option>
              <option>S</option>
              <option>M</option>
              <option>L</option>
              <option>XL</option>
            </select>
            
            <button class="add-to-cart" on:click={() => addToCart(product)}>
              Hinzufügen
            </button>
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
  /* All your existing wishlist styles */
  .wishlist-overlay {
    position: fixed;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    background: rgba(0, 0, 0, 0.5);
    z-index: 1001;
    animation: fadeIn 0.3s ease;
  }

  .wishlist-slider {
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

  .wishlist-header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 1.5rem 2rem;
    background-image: linear-gradient(to bottom right, #e1d7bd, #e5dcc6, #efeade);
    border-bottom: 1px solid rgba(206, 47, 36, 0.2);
  }

  .wishlist-header h2 {
    margin: 0;
    color: #ce2f24;
    font-size: 1.5rem;
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

  .wishlist-content {
    flex: 1;
    overflow-y: auto;
    padding: 1.5rem;
    scrollbar-width: thin;
    scrollbar-color: #ce2f24 #f3f6fb;
  }

  .wishlist-content::-webkit-scrollbar {
    width: 6px;
  }

  .wishlist-content::-webkit-scrollbar-track {
    background: #f3f6fb;
  }

  .wishlist-content::-webkit-scrollbar-thumb {
    background: #ce2f24;
    border-radius: 3px;
  }

  .empty-wishlist {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    height: 100%;
    color: #999;
    gap: 1rem;
    text-align: center;
    padding: 2rem;
  }

  .empty-wishlist :global(svg) {
    opacity: 0.3;
    color: #ce2f24;
  }

  .empty-wishlist p {
    margin: 0;
    font-size: 1.1rem;
    font-weight: 600;
    color: #666;
  }

  .empty-wishlist small {
    color: #999;
    font-size: 0.9rem;
  }

  .wishlist-item {
    display: flex;
    gap: 1rem;
    padding: 1rem;
    border-bottom: 1px solid #eee;
    transition: background-color 0.2s;
  }

  .wishlist-item:hover {
    background-color: #fafafa;
  }

  .wishlist-item img {
    width: 100px;
    height: 130px;
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
    font-size: 0.95rem;
    font-weight: 600;
    color: #333;
    line-height: 1.3;
  }

  .item-price {
    display: flex;
    align-items: center;
    gap: 0.5rem;
  }

  .item-price .price {
    color: #ce2f24;
    font-weight: 600;
    font-size: 1rem;
  }

  .item-price .original {
    color: #999;
    font-size: 0.875rem;
    text-decoration: line-through;
  }

  .remove-btn {
    align-self: flex-start;
    background: transparent;
    border: 1px solid #ddd;
    padding: 0.5rem 1rem;
    border-radius: 4px;
    cursor: pointer;
    font-size: 0.875rem;
    transition: all 0.2s;
    margin-top: auto;
  }

  .remove-btn:hover {
    background: #f5f5f5;
    border-color: #ce2f24;
    color: #ce2f24;
  }

  .wishlist-footer {
    padding: 1.5rem 2rem;
    border-top: 2px solid #eee;
    background: #fafafa;
  }

  .item-count {
    margin: 0 0 1rem 0;
    font-size: 0.95rem;
    color: #666;
    text-align: center;
  }

  .continue-btn {
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

  .continue-btn:hover {
    background: #a52419;
    transform: translateY(-2px);
    box-shadow: 0 4px 12px rgba(206, 47, 36, 0.3);
  }

  /* Carousel styles */
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
    min-width: 230px;
    flex-shrink: 0;
    display: flex;
    flex-direction: column;
    width: 20%;
  }

  .product-image {
    position: relative;
    background-color: #fff;
    aspect-ratio: 3/4;
    overflow: hidden;
    margin-bottom: 0.75rem;
    width: 100%;
    height: 80%;
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
    transition: all 0.3s;
    box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
  }

  .favorite-btn:hover {
    transform: scale(1.1);
    box-shadow: 0 4px 12px rgba(0, 0, 0, 0.15);
  }

  .favorite-btn.active {
    background: #ffe6e6;
    animation: heartBeat 0.3s ease;
  }

  @keyframes heartBeat {
    0%, 100% {
      transform: scale(1);
    }
    25% {
      transform: scale(1.2);
    }
    50% {
      transform: scale(1.1);
    }
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
    margin-left: 0.32rem;
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
    transition: all 0.3s;
  }

  .add-to-cart:hover {
    background-color: #fff;
    color: #000;
    border: 1px solid rgba(102, 102, 102);
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
    box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
    z-index: 10;
    transition: all 0.2s;
  }

  .scroll-btn:hover {
    background-color: #f5f5f5;
    box-shadow: 0 4px 12px rgba(0, 0, 0, 0.15);
  }

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
</style>
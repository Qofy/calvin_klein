<script>
  import { Heart } from "lucide-svelte";
  
  export let data;
  
  const { breadcrumbs, title, price, colors, sizes, fitGuide, payment, details, shipping } = data;
  
  let selectedColor = colors[0].name;
  let selectedSize = "";
  let showDetails = false;
  let showShipping = false;
  
  function toggleDetails() {
    showDetails = !showDetails;
  }
  
  function toggleShipping() {
    showShipping = !showShipping;
  }
</script>

<div class="product-details">
  <!-- Breadcrumb -->
  <div class="breadcrumb">
    {breadcrumbs.map(b => b.label).join(' - ')}
  </div>

  <!-- Product Title -->
  <h1>{title}</h1>

  <!-- Price -->
  <div class="price-section">
    <div class="current-price">{price.current} <span class="vat">{price.vat}</span></div>
    <div class="price-info">
      <p>Niedrigster Preis der letzten 30 Tage: {price.lowest30Days}</p>
      <p>Ursprünglich verkauft für: {price.original}</p>
    </div>
  </div>

  <!-- Color Selection -->
  <div class="color-section">
    <h3>Farbe: <span class="selected">{selectedColor}</span></h3>
    <div class="color-options">
      {#each colors as color}
        <button 
          class="color-option"
          class:active={selectedColor === color.name}
          on:click={() => selectedColor = color.name}
        >
          <img src={color.image} alt={color.name} />
        </button>
      {/each}
    </div>
  </div>

  <!-- Size Selection -->
  <div class="size-section">
    <h3>Größe:</h3>
    <div class="size-options">
      {#each sizes as size}
        <button
          class="size-option"
          class:active={selectedSize === size}
          on:click={() => selectedSize = size}
        >
          {size}
        </button>
      {/each}
    </div>
    <a href="#" class="size-guide">Größen-Guide</a>
  </div>

  <!-- Add to Cart Buttons -->
  <div class="cart-buttons">
    <button class="add-to-cart">Hinzufügen</button>
    <button class="favorite-btn">
      <Heart size={24} />
    </button>
  </div>

  <!-- Payment Info -->
  <div class="payment-info">
    <p>{payment.text} <strong>{payment.provider}</strong></p>
    <a href={payment.learnMoreLink} class="learn-more">Mehr erfahren</a>
  </div>

  <!-- Fit Guide -->
  <div class="fit-guide">
    <h4>{fitGuide.title}</h4>
    <p>{fitGuide.description}</p>
    <div class="fit-slider">
      <span class="fit-label left">{fitGuide.scale.labels[0]}</span>
      <div class="slider-track">
        <div class="slider-indicator"></div>
      </div>
      <span class="fit-label center">{fitGuide.scale.labels[1]}</span>
      <span class="fit-label right">{fitGuide.scale.labels[2]}</span>
    </div>
  </div>

  <!-- Details Section -->
  <div class="accordion-section">
    <button class="accordion-header" on:click={toggleDetails}>
      <span>Details</span>
      <span class="icon">{showDetails ? '−' : '+'}</span>
    </button>
    {#if showDetails}
      <div class="accordion-content">
        <p>{details.description}</p>
        
        <ul>
          {#each details.features as feature}
            <li>• {feature}</li>
          {/each}
        </ul>
        
        <p>{details.material}<br>
        {#each details.care as care}
          {care}<br>
        {/each}
        </p>
        
        <p>Herstellungsland: {details.origin}</p>
        
        <p>{details.returnPolicy}</p>
        
        <p class="product-code">{details.sku}</p>
      </div>
    {/if}
  </div>

  <!-- Shipping Section -->
  <div class="accordion-section">
    <button class="accordion-header" on:click={toggleShipping}>
      <span>{shipping.title}</span>
      <span class="icon">{showShipping ? '−' : '+'}</span>
    </button>
    {#if showShipping}
      <div class="accordion-content">
        <p>{shipping.content}</p>
      </div>
    {/if}
  </div>
</div>


<style>
  .product-details {
    padding: 2rem;
    max-width: 600px;
    /* overflow-y: scroll; */
  }

  /* Breadcrumb */
  .breadcrumb {
    color: #999;
    font-size: 0.875rem;
    margin-bottom: 2rem;
  }

  /* Title */
  h1 {
    font-size: 2rem;
    font-weight: 400;
    margin-bottom: 1rem;
    letter-spacing: 0.5px;
    color: #ce2f24;

  }

  /* Price Section */
  .price-section {
    margin-bottom: 2rem;
  }

  .current-price {
    font-size: 1.25rem;
    font-weight: 600;
    margin-bottom: 0.5rem;
  }

  .vat {
    font-size: 0.875rem;
    font-weight: 400;
    color: #666;
  }

  .price-info {
    color: #666;
    font-size: 0.875rem;
  }

  .price-info p {
    margin: 0.25rem 0;
  }

  /* Color Section */
  .color-section {
    margin-bottom: 2rem;
  }

  .color-section h3 {
    font-size: 1rem;
    font-weight: 400;
    margin-bottom: 1rem;
    color: #ce2f24;

  }

  .selected {
    font-weight: 600;
    color: #000;
  }

  .color-options {
    display: flex;
    gap: 1rem;
  }

  .color-option {
    width: 80px;
    height: 100px;
    border: 2px solid transparent;
    cursor: pointer;
    padding: 0;
    background: none;
    transition: border-color 0.2s;
  }

  .color-option.active {
    border-color: #000;
  }

  .color-option img {
    width: 100%;
    height: 100%;
    object-fit: cover;
  }

  /* Size Section */
  .size-section {
    margin-bottom: 2rem;
  }

  .size-section h3 {
    font-size: 1rem;
    font-weight: 400;
    margin-bottom: 1rem;
    color: #ce2f24;

  }

  .size-options {
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    gap: 1rem;
    margin-bottom: 1rem;
  }

  .size-option {
    padding: 1rem;
    border: 1px solid #ddd;
    background: white;
    font-size: 1rem;
    cursor: pointer;
    transition: all 0.2s;
  }

  .size-option:hover {
    border-color: #000;
  }

  .size-option.active {
    background-color: #000;
    color: white;
    border-color: #000;
  }

  .size-guide {
        color: #ce2f24;
    text-decoration: underline;
    font-size: 0.875rem;
  }

  /* Cart Buttons */
  .cart-buttons {
    display: flex;
    gap: 1rem;
    margin-bottom: 1.5rem;
  }

  .add-to-cart {
    flex: 1;
    padding: 1rem;
    background-color: #ce2f24;
    color: white;
    border: none;
    font-size: 1rem;
    font-weight: 500;
    cursor: pointer;
    transition: background-color 0.2s;
  }

  .add-to-cart:hover {
    background-color: #fff;
    color: #000;
    border: 1px solid rgba(102, 102, 102);
  }

  .favorite-btn {
    padding: 1rem;
    background: white;
    border: 1px solid #000;
    cursor: pointer;
    display: flex;
    align-items: center;
    justify-content: center;
    transition: all 0.2s;
  }

  .favorite-btn:hover {
    background-color: #f5f5f5;
  }

  /* Payment Info */
  .payment-info {
    margin-bottom: 2rem;
    padding-bottom: 2rem;
    border-bottom: 1px solid #e0e0e0;
  }

  .payment-info p {
    margin-bottom: 0.5rem;
    font-size: 0.875rem;
  }

  .learn-more {
    color: #ce2f24;
    text-decoration: underline;
    font-size: 0.875rem;
  }

  /* Fit Guide */
  .fit-guide {
    margin-bottom: 2rem;
    padding-bottom: 2rem;
    border-bottom: 1px solid #e0e0e0;
  }

  .fit-guide h4 {
    font-size: 1rem;
    font-weight: 600;
    margin-bottom: 0.5rem;
    color: #ce2f24;
  }

  .fit-guide p {
    font-size: 0.875rem;
    color: #666;
    margin-bottom: 1rem;
  }

  .fit-slider {
    display: grid;
    grid-template-columns: auto 1fr auto;
    align-items: center;
    gap: 1rem;
    position: relative;
  }

  .fit-label {
    font-size: 0.75rem;
    color: #666;
  }

  .fit-label.left {
    grid-column: 1;
  }

  .fit-label.center {
    position: absolute;
    left: 50%;
    transform: translateX(-50%);
    top: -1.5rem;
  }

  .fit-label.right {
    grid-column: 3;
  }

  .slider-track {
    grid-column: 1 / 4;
    height: 2px;
    background-color: #ddd;
    position: relative;
    margin: 0.5rem 0;
  }

  .slider-indicator {
    position: absolute;
    left: 10%;
    top: 50%;
    transform: translateY(-50%);
    width: 12px;
    height: 12px;
    background-color: #000;
    border-radius: 50%;
  }

  /* Accordion Section */
  .accordion-section {
    border-bottom: 1px solid #e0e0e0;
  }

  .accordion-header {
    width: 100%;
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 1.5rem 0;
    background: none;
    border: none;
    font-size: 1rem;
    font-weight: 400;
    cursor: pointer;
    text-align: left;
  }

  .accordion-header .icon {
    font-size: 1.5rem;
    font-weight: 300;
  }

  .accordion-content {
    padding-bottom: 1.5rem;
    font-size: 0.875rem;
    line-height: 1.6;
  }

  .accordion-content p {
    margin-bottom: 1rem;
  }

  .accordion-content ul {
    list-style: none;
    padding: 0;
    margin: 1rem 0;
  }

  .accordion-content li {
    margin-bottom: 0.5rem;
  }

  .product-code {
    color: #666;
    margin-top: 1rem;
  }

  @media (max-width: 768px) {
    .product-details {
      padding: 1rem;
    }

    h1 {
      font-size: 1.5rem;
    }

    .size-options {
      grid-template-columns: repeat(3, 1fr);
    }
  }
</style>
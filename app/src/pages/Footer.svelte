<script>
  import { Check, Globe } from "lucide-svelte";
  
  export let data;
  
  const { newsletter, columns, languageSelector, copyright, socialLinks } = data;
</script>

<!-- <footer> -->
  <!-- Newsletter Section -->
  <div class="newsletter-section"> 
    <h2>{newsletter.title}</h2>
    
    <div class="benefits">
      {#each newsletter.benefits as benefit}
        <div class="benefit">
          <Check size={16} />
          <span>{benefit}</span>
        </div>
      {/each}
    </div>
    
    <button class="signup-btn">{newsletter.ctaButton}</button>
  </div>

  <!-- Footer Links Section -->
  <div class="footer-content">
    {#each columns as column}
      <div class="footer-column">
        <h3>{column.title}</h3>
        <ul>
          {#each column.links as link}
            <li><a href={link.href}>{link.label}</a></li>
          {/each}
        </ul>
      </div>
    {/each}
    
    <div class="footer-column">
      <h3>{languageSelector.label}</h3>
      <div class="language-selector">
        <Globe size={20} />
        <span>{languageSelector.current}</span>
      </div>
    </div>
  </div>

  <!-- Footer Bottom -->
  <div class="footer-bottom">
    <p>{copyright}</p>
    
    <div class="social-icons">
      {#each socialLinks as social}
        <a href={social.href} aria-label={social.aria}>
          <!-- Keep your existing SVG icons here -->
        </a>
      {/each}
    </div>
   </div> 
<!-- </footer> -->


<style>
  /* footer {
    background-color: #fbb900;
    color: #e43417;
    padding: 0;
  }

  
  .newsletter-section {
    text-align: center;
    padding: 4rem 2rem;
    border-bottom: 1px solid #333;
  } */

  .newsletter-section h2 {
    font-size: clamp(1.5rem, 4vw, 2rem);
    font-weight: 400;
    margin-bottom: 2rem;
    letter-spacing: 0.5px;
  }

  .benefits {
    display: flex;
    justify-content: center;
    gap: 2rem;
    margin-bottom: 2rem;
    flex-wrap: wrap;
  }

  .benefit {
    display: flex;
    align-items: center;
    gap: 0.5rem;
    font-size: 0.95rem;
  }

  .signup-btn {
    background-color: #e43417;
    color: #fff;
    border: none;
    padding: 0.875rem 3rem;
    font-size: 0.95rem;
    font-weight: 500;
    cursor: pointer;
    transition: all 0.3s;
  }

  .signup-btn:hover {
    background-color: #fff;
    color: #000;
  }

  /* Footer Content */
  .footer-content {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
    gap: 3rem;
    padding: 3rem 2rem;
    max-width: 1400px;
    margin: 0 auto;
  }

  .footer-column h3 {
    font-size: 0.875rem;
    font-weight: 600;
    margin-bottom: 1.5rem;
    text-transform: uppercase;
    letter-spacing: 0.5px;
  }

  .footer-column ul {
    list-style: none;
    padding: 0;
    margin: 0;
  }

  .footer-column li {
    margin-bottom: 0.75rem;
  }

  .footer-column a {
    color: #fff;
    text-decoration: none;
    font-size: 0.875rem;
    transition: opacity 0.2s;
  }

  .footer-column a:hover {
    opacity: 0.7;
  }

  .language-selector {
    display: flex;
    align-items: center;
    gap: 0.5rem;
    cursor: pointer;
    transition: opacity 0.2s;
  }

  .language-selector:hover {
    opacity: 0.7;
  }

  /* Footer Bottom */
  .footer-bottom {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 2rem;
    /* border-top: 1px solid #333; */
    flex-wrap: wrap;
    gap: 1rem;
  }

  .footer-bottom p {
    font-size: 0.875rem;
    margin: 0;
  }

  .social-icons {
    display: flex;
    gap: 1.5rem;
    align-items: center;
  }

  .social-icons a {
    color: #fff;
    transition: opacity 0.2s;
    display: flex;
    align-items: center;
  }

  .social-icons a:hover {
    opacity: 0.7;
  }

  @media (max-width: 768px) {
    .benefits {
      flex-direction: column;
      align-items: center;
      gap: 1rem;
    }

    .footer-content {
      grid-template-columns: repeat(2, 1fr);
      gap: 2rem;
    }

    .footer-bottom {
      flex-direction: column;
      text-align: center;
    }
  }

  @media (max-width: 480px) {
    .footer-content {
      grid-template-columns: 1fr;
    }
  }
</style>
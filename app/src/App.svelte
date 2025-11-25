<script>
  import {Search, Globe, Heart, UserRound, ShoppingBag} from "lucide-svelte"

  import bk1 from "../public/assets/bike/b1.png"
import bk2 from "../public/assets/bike/b2.png"
// import bk3 from "../public/assets/bike/b3.png"
// import bk4 from "../public/assets/bike/b4.png"

</script>

<main>
  <nav>
    <div class="nav">
      <a href="#">Damen</a>
      <a href="#">Herren</a>
      <a href="#">Kinder</a>
      <a href="#">Black Friday</a>
    </div>
    
    <div>
      <svg class="Icon_Icon__qPZ8O Icon_regular__MbCqv" 
        data-testid="brand-logo-svg" width="115" height="19" viewBox="0 0 115 19" fill="none" xmlns="http://www.w3.org/2000/svg">
        <path fill-rule="evenodd" clip-rule="evenodd" 
          d="M82.8954 18.2007H84.708V0.61412H82.8954V18.2007ZM71.4005 12.7452L73.5803 10.2821L79.5685 18.2008H81.8628L74.9567 8.74004L81.8628 0.9365H79.4767L71.4005 10.144V0.9365H69.4046V18.2008H71.4005V12.7452ZM48.4799 18.2007H50.2925V6.0926H48.4799V18.2007ZM48.457 3.9749H50.3155V1.8572H48.457V3.9749ZM54.3074 18.2008H52.4951V6.0926H54.3074V8.11832C54.5369 7.45088 55.5924 5.81648 58.0931 5.81648C61.4658 5.81648 63.0489 8.30246 63.0489 11.3641V18.2008H61.2136V11.4102C61.2136 9.13118 59.9975 7.54286 57.7949 7.54286C55.6153 7.54286 54.3074 9.17726 54.3074 11.5021V18.2008ZM96.6614 10.9956H88.3789C88.6772 9.26924 90.1914 7.49696 92.5316 7.49696C94.9407 7.49696 96.2943 9.17726 96.6614 10.9956ZM86.4287 12.1467C86.4287 15.7377 89.0443 18.477 92.5775 18.477C96.2024 18.477 97.9922 15.9678 98.4511 14.3105H96.6384C96.1565 15.3234 94.9866 16.7736 92.5775 16.7736C90.1684 16.7736 88.4018 14.9319 88.264 12.607H98.6115C98.7034 8.64788 96.065 5.81648 92.5316 5.81648C89.0672 5.81648 86.4287 8.57876 86.4287 12.1467ZM100.379 18.2007H102.191V6.0926H100.379V18.2007ZM100.356 3.9749H102.214V1.8572H100.356V3.9749ZM104.394 18.2008H106.206V11.5021C106.206 9.17726 107.514 7.54286 109.693 7.54286C111.896 7.54286 113.112 9.13118 113.112 11.4102V18.2008H114.947V11.3641C114.947 8.30246 113.364 5.81648 109.992 5.81648C107.491 5.81648 106.435 7.45088 106.206 8.11832V6.0926H104.394V18.2008ZM2.06498 9.59162C2.06498 13.6198 4.95576 16.6354 8.74144 16.6354C12.2747 16.6354 14.0183 14.4486 14.5691 13.3668H16.5652C16.0604 15.024 13.6742 18.5 8.74144 18.5C3.76271 18.5 0 14.7249 0 9.56858C0 4.48142 3.80863 0.63716 8.74144 0.63716C13.6742 0.63716 16.0604 4.04402 16.611 5.81648H14.5462C13.9267 4.6886 12.2058 2.50178 8.74144 2.50178C4.95576 2.50178 2.06498 5.51732 2.06498 9.59162ZM23.8156 7.54286C26.3163 7.54286 28.1519 9.54554 28.1519 12.1467C28.1519 14.7479 26.3163 16.7506 23.8156 16.7506C21.2919 16.7506 19.4564 14.7479 19.4564 12.1467C19.4564 9.5225 21.2919 7.54286 23.8156 7.54286ZM17.598 12.1467C17.598 15.7608 20.3053 18.477 23.7467 18.477C26.4771 18.477 27.7389 16.7506 28.1289 15.9217V18.2008H29.9414V6.0926H28.1289V8.37158C27.7618 7.5659 26.4771 5.81648 23.7467 5.81648C20.3053 5.81648 17.598 8.53268 17.598 12.1467ZM32.1444 18.2007H33.9568V0.61412H32.1444V18.2007ZM44.9924 6.0926L41.1608 16.3362L37.3292 6.0926H35.3333L40.0137 18.201H42.3082L46.9885 6.0926H44.9924Z" fill="#1A1919">
        </path>
      </svg>
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
     <div style="background-image: url({bk1});"></div>
        <div style="background-image: url({bk2});"></div>
        <!-- <div style="background-image: url({bk3});"></div>
        <div style="background-image: url({bk4});"></div> -->
  </div>
  
  <div class="sidebar">

  </div>
  <div class="four">sidbckjsvk</div>
  <div class="five">vdkjdkfj</div>
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
    background-color: #fff;
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
  }

  .hero div{
    background-position: center;
    background-repeat: no-repeat;
    background-size:cover;
    height: 40rem;
}
  
  .sidebar{
    background-color: burlywood;
    grid-column: 4 / 6;
    grid-row: 2 / 7;
  }
  
  .four{
    background-color: cadetblue;
    grid-column: 1 / 6;
    grid-row: 7 / 9;
  }

  .five{
    background-color: brown;
    grid-row: 9 / 11;
    grid-column: 1 / 6;
  }
</style>
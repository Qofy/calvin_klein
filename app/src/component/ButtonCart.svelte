<script>
import {Heart} from "lucide-svelte"
import App from "../App.svelte";
</script>

<div class="buttonCart">
  <button class="add-button">Hinzufügen</button>
  <button class="heart-button">
    <Heart/>
  </button>
</div>

<style>
  .buttonCart{
    display: flex;
    align-items: center;
    gap: 1rem;
  }
  
  .add-button{
    color: white;
    background-color: black;
    border: 1px solid black;
    padding: 0.75rem 5rem;
    cursor: pointer;
    font-weight: 500;
  }
  
  .add-button:hover{
    background-color: #fff;
    color: #000;
  }
  
  .heart-button{
    background: transparent;
    border: 1px solid #ccc;
    padding: 0.75rem;
    cursor: pointer;
    display: flex;
    align-items: center;
    justify-content: center;
  }
  
  .heart-button:hover{
    border-color: #000;
  }
</style>
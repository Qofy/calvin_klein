<script>
import {Truck, Package} from "lucide-svelte"
  import App from "../App.svelte";
</script>

<div class="card-promo">
<p class="concept">In bis zu 30 Tagen bezahlen. Sicher mit 
    <strong>Klarna</strong> 
    <a href="#">Mehr erfahren</a>
</p>
<div class="content_shopping">
    <p><Truck/>
        <a href="#">Kostenlose Lieferung ab einem Bestellwert von 50 €</a>
    </p>
     <p><Package/>
        <a href="#">60 Tage kostenlose Rückgabe</a>
    </p>
</div>
</div>

<style>
.card-promo{
    display: flex;
    flex-direction: column;
    gap: 2rem;

}

.card-promo .concept{
    width: 390px;
}

.content_shopping{
    display: flex;
    flex-direction: column;
    gap: 1rem;
    
}
.content_shopping p{
    display: flex;
    align-items: center;
    gap: .6rem;
}

.concept a{
    text-decoration: underline;
}
</style>
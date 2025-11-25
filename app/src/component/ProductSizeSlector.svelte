<script>

</script>

<div class="size-selector">
<p>
    Größe:
</p>
<div class="sizes">
    <div>XS</div>
    <div>S</div>
    <div>M</div>
    <div>L</div>
    <div>Xl</div>
</div>
<a href="#">
    Größen-Guide
</a>
</div>

<style>
.size-selector {
    display: flex;
    flex-direction: column;
    gap: 2rem;
}
.size-selector p{
    color: rgba(102,102,102);
}
.sizes{
    display: flex;
    gap: 0.8rem;
}
.sizes div{
    border: 1px solid black;
    width: 100px;
    height: 60px;
    display: flex;
    align-items: center;
    justify-content: center;
    font-weight: 100;
    font-size: .8rem;

}

a{
    text-decoration: underline;
}
</style>
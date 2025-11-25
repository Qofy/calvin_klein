<script>

const siderLinks =[
    "Damen","Unterwäsche","Unterhosen","Bikinislips"
]
$: sideLink=siderLinks.map(item=>`<a href="#">${item}</a>`)
</script>

<main>
    <div class="links">
       {@html sideLink.join("")}
    </div>
</main>

<style>

</style>
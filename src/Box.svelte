<style>
    .box {
        width: 300px;
        border: 2px solid #aaa;
        border-radius: 40px;
        padding: 2rem;
        background: white;
    }
    header,article {
        font-weight: bold;
    }
</style>


<div class="box">
    <slot />

    <header>    
        <slot name="header"/>
    </header>
    <article>    
		<span>Halo Lurrr Body</span>
    </article>
    <footer>     
        <slot name="footer"/>
    </footer>
</div>


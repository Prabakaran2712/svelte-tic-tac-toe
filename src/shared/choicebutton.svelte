<script>
 export let choice;
</script>
<main>
<div class="xo" on:click>
    <button>{choice}</button>
</div>
</main>
<style>
 
 
.xo{
    width: 100px;
    height: 100px;
text-align: center;
padding: 20px;

}
.xo button:hover{
    background-color: aliceblue;
    color: #777;
    border: 2px solid #777;
}
.xo button{
    text-transform: uppercase;
    border-radius: 10px;
    font-size: large;
    width: 100px;
    height: 100px;
    background-color: #777;
    color: aliceblue;
}
</style>
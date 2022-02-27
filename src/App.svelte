<script>
	import Button from  './shared/choicebutton.svelte';
	import { fade, fly } from 'svelte/transition';
	$: name="";
	let page="page1";
	let choice;
	let board=[{id:1,value:""},{id:2,value:""},{id:3,value:""},{id:4,value:""},{id:5,value:""},{id:6,value:""},{id:7,value:""},{id:8,value:""},{id:9,value:""}];
	let error='';
    let ef=0;
	let winner='';
    const click=(id)=>{
        fullcheck();
        if(checkempty(id)){
            error='';
        if(choice=='x'){
            for(var i=0;i<board.length;i++){
                if(id===board[i].id && board[i].value===''){
                    board[i].value="x";
                    
                }
                
            }
            if(!fullcheck()){
            while(1){
               let r=Math.floor(Math.random() * 8);
console.log(r);
                if(board[r].value!=""){
                    r=Math.floor(Math.random() * 8);
                }
                else{
                    
                    board[r].value="y";
                    break;
                }
            }
        }
        }
        else if(choice=='y'){
          
            for(var i=0;i<board.length;i++){
                if(id===board[i].id && board[i].value===''){
                    board[i].value="y";
                    
                }
                
            }
            if(!fullcheck()){
            while(1){
               let r=Math.floor(Math.random() * 8);
console.log(r);
                if(board[r].value!=""){
                    r=Math.floor(Math.random() * 8);
                }
                else{
                    
                    board[r].value="x";
                    break;
                }
            }
        }
        }
        else{
 error="Enter a valid choice";
        }
    }
    else{
      
error="already taken";
return;
    }
	console.log("hi");
	wincheck();
	return;
	
}
    const fullcheck=()=>{
        let boardcopy=board.filter((x)=>x.value=='');
        console.log(boardcopy);
        if(boardcopy.length===0){
            
            return true;
        }
        return false;
    }
	const wincheck=()=>{
		if(board[0].value===board[1].value && board[1].value ===board[2].value && board[0].value != ''){
       console.log( board[0].value);
	   winner=board[0].value;
	   page="result";
	   return;
	    }
    else if(board[3].value === board[4].value && board[4].value === board[5].value && board[3].value != '') {   
	console.log( board[3].value);
	winner=board[3].value;
	   page="result";
	   return;  }  
    else if(board[6].value === board[7].value && board[7].value === board[8].value && board[6].value != '') {   
		console.log( board[6].value);
		winner=board[6].value;
	   page="result";
	   return;   
	}
    else if(board[0].value === board[3].value && board[3].value === board[6].value && board[0].value != ''){
		console.log( board[0].value);
		winner=board[0].value;
	   page="result";
	   return;    
	}
    else if(board[1].value === board[4].value && board[4].value === board[7].value && board[1].value != ''){    
		console.log( board[1].value);
		winner=board[1].value;
	   page="result";
	   return;    }
    else if(board[2].value === board[5].value && board[5].value === board[8].value && board[2].value != ''){
		console.log( board[2].value);
		winner=board[2].value;
	   page="result";
	   return;
	}
    
    else if(board[0].value === board[4].value && board[4].value === board[8].value && board[4].value!= ''){
		console.log( board[0].value);
		winner=board[0].value;
	   page="result";
	   return;
	}    
         
    else if(board[2].value === board[4].value && board[4].value === board[6].value && board[4].value != ''){
		console.log( board[2].value);
		winner=board[2].value;
	   page="result";
	   return;
	}
    else if(board[1].value!='' && board[2].value!='' && board[3].value!='' && board[4].value!='' && board[5].value!='' && board[6].value!='' && board[7].value!='' && board[8].value!='' && board[0].value!=''){
		console.log("Draw");
		winner="none";
	   page="result";
		return;
	}    
	else{
		console.log("running");
	}
	}
    const checkempty=(id)=>{
        let boardcop=board.filter((x)=>{return(x.id===id && x.value!='');});
        console.log(boardcop);
        if(boardcop.length===0){
            return true;
        }
        else{
 return false;
        }
    }
</script>

<main>
	{#if page==="page1"}
	<div class="page1" transition:fade>
		<h1>TIC TAC TOE</h1>
		<h4>Enter your Name </h4>
		<input type="text"  bind:value={name}>
		<h5 class="error">{error}</h5>
		
		<div class="button">
		<button on:click={()=>{if(name.length>=5){page="welcome"; error="";board=[{id:1,value:""},{id:2,value:""},{id:3,value:""},{id:4,value:""},{id:5,value:""},{id:6,value:""},{id:7,value:""},{id:8,value:""},{id:9,value:""}];}else{error= "Name should contain minimum 5 characters";}}}>CONTINUE</button></div>
	</div>
    {:else if page=="welcome"}
	<div class="welcome" transition:fade>
	<h2>
		WELCOME {name}
	</h2>
	<button on:click={()=>{page="choice";}}>CONTINUE</button>
	</div>
	{:else if page=="choice"}
	<div class="choice-body">
		<h2>CHOOSE X OR Y</h2>
	<div class="choice">
<Button choice={'x'} on:click={()=>{page='choice_notification'; choice='x'}}></Button>
<Button choice={'y'} on:click={()=>{page='choice_notification'; choice='y'}}></Button>
	</div></div>
	{:else if page=="choice_notification"}
	<h2>You have chosen {choice}</h2>
	<button on:click={()=>{page="game";}}>CONTINUE</button>
	{:else if page=="game"}
	<div class="game">
	<h1>Game </h1>
	<div class="grid-container" transition:fade>
		{#each board as member }
		   <div class="grid-item" on:click={()=>{click(member.id)}}>{member.value}</div>
		{/each}
	  </div> 
	  <div class="error">{error}</div>
	  </div>
	  {:else if page=="result" }
	  <div class="result" transition:fade>
	  {#if winner!="none"}
	   <h2>{winner} is the Winner</h2>
	   {:else}
	   <h1>Match is Draw</h1>
	   {/if}
	   <button on:click={()=>{page="page1";}}>HOME</button>
	   </div>
	{/if}
</main>

<style>
	main {
		text-align: center;
		padding: 1em;
		max-width: 240px;
		margin: 0 auto;
	}
	.error{
		color: rgba(255, 60, 0, 0.959);
	}
.choice{
	display: flex;
	flex-direction: row;
	margin: 10px 40%;
}
	h1 {
		color: #f69526;
		text-transform: uppercase;
		font-size: 4em;
		font-weight: 100;
	}
	h2 {
		color: #f69526;
		text-transform: uppercase;
		font-size: 4em;
		font-weight: 100;
	}
button{
	padding: 10px;
	border-radius: 10px;
	background-color:rgb(45, 177, 45);
	border: 2px solid white;
	color: aliceblue;
	font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
}
button:hover{
background-color: white;
border-color: rgb(45, 177, 45);
color:rgb(45, 177, 45);
}
	@media (min-width: 640px) {
		main {
			max-width: none;
		}
	}
	.grid-container {
  display: grid;
  grid-template-columns: auto auto auto;
  background-color: #f69526;
  padding: 10px;
}
.grid-item {
  background-color: rgba(255, 255, 255, 0.8);
  border: 1px solid #f69526;
  text-transform: uppercase;
  padding: 20px;
  font-size: 30px;
  text-align: center;
  min-width: 100px;
  min-height: 100px;
}
</style>
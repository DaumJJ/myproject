
<script>




	 let name='todo list';
	//  let beltcolour='black';

    let todos=[]
	let persons=[]
	function add(){
     todos=[...todos,""]
	 }


		let people = [
		{ num: '1', names: 'Rom',score:'99' },
		{ num: '2',names: 'Deils',score:'98'},
		{ num: '2', names: 'Tisch',score:'90'}
	];

	let prefix = '';
	let num = '';
	let names= '';
	let score='';
	let i = 0;

	$: filteredPeople = prefix
		? people.filter(person => {
			const name = `${person.num}, ${person.names},${person.score}`;
			return name.toLowerCase().startsWith(prefix.toLowerCase());
		})
		: people;

	$: selected = filteredPeople[i];

	$: reset_inputs(selected);



	function create() {
		people = people.concat({ num, names,score });
		i = people.length - 1;
		num = names =score= '';
	}

	function update() {
		selected.num = num;
		selected.names = names;
		selected.score = score;
		people = people;
	}

	function remove() {
		// Remove selected person from the source array (people), not the filtered array
		const index = people.indexOf(selected);
		people = [...people.slice(0, index), ...people.slice(index + 1)];

		num = names =score='';
		i = Math.min(i, filteredPeople.length - 2);
	}

	function reset_inputs(person) {
		num = person ? person.num : '';
		names = person ? person.names : '';
		score = person ? person.score : '';
	}


	 import Modal from './Modal.svelte';
	 import Modal2 from './Modal2.svelte';
      let showModal = false;
	  let showModal2 = false;

</script>


{#if showModal}
	<Modal on:close="{() => showModal = false}">
		<h2 slot="header">
		   人员添加
		
		</h2>

		
		<label class="putin"><p>请输入编号：</p><input bind:value={num} placeholder="num"></label>
		<label class="putin"><p>请输入姓名：</p><input bind:value={names} placeholder="names"></label>
		<label class="putin"><p>请输入成绩：</p><input bind:value={score} placeholder="score"></label>
		<div class='buttons' style="margin-left:460px;">
			<button on:click={create} disabled="{!num || !names || !score}" style=" background-color:#2da04d; /* Green */
			border-radius:5px;
			color: #fffff4;
			padding:5px 10px;
			text-align: center;
			text-decoration: none;
			display: inline-block;
			font-size: 14px;">确定</button>
		
		</div>
	
	</Modal>
{/if}


{#if showModal2}
	<Modal2 on:close="{() => showModal2 = false}">
		<h2 slot="header">
		   修改列表
		
		</h2>

		
		<label class="putin"><p>请输入编号：</p><input bind:value={num} placeholder="num"></label>
		<label class="putin"><p>请输入姓名：</p><input bind:value={names} placeholder="names"></label>
		<label class="putin"><p>请输入成绩：</p><input bind:value={score} placeholder="score"></label>
		<div class='buttons' style="margin-left:460px;">
			<button on:click={update} disabled="{!num || !names || !score}" style=" background-color:#2da04d; /* Green */
			border-radius:5px;
			color: #fffff4;
			padding:5px 10px;
			text-align: center;
			text-decoration: none;
			display: inline-block;
			font-size: 14px;">修改</button>
		
		</div>
	
	</Modal2>
{/if}



<main>
	

	 <h1>Welcome {name}!</h1> 
	 <input placeholder="Please enter what you want to search number" bind:value={prefix} style="float:left; width:400px;">


		<button on:click="{() => showModal = true}" style="float:right;background-color: #2da04d; /* Green */
			border-radius:5px;
			color: #fffff4;
			padding: 8px 30px;
			text-align: center;
			text-decoration: none;
			display: inline-block;
			font-size: 16px;Font Family:'黑体'；" > 
			添加
		</button>
	
	
    <table border="1">
		<tr>
		  <th>编号</th>
		  <th>姓名</th>
		  <th>得分</th>
		  <th>编辑</th>
		  <th>删除</th>
		</tr>
		{#each filteredPeople as person, i}
			<tr>
			
				<th>{person.num}</th>
				<th>{person.names}</th>
				<th>{person.score}</th>
				<th><button  on:click="{() => showModal2 = true}" disabled="{!num || !names || !score|| !selected}" style="background-color:#f6f8fa;font-family: 'Times New Roman', Times, serif;font-weight:bold;">update</button></th>
				<th><button on:click={remove} disabled="{!selected}" style="background-color:#ce4308; padding:5px 10px;border:none;color:white;">×</button></th>
				<!-- <th><button on:click="{() => remove(todo)}">x</button></th> -->
	
			</tr>
		{/each}
	  </table>






</main>

<style>
	main {
	
		padding: 1em;
		max-width: 100%;
		margin: 0 auto;
	}

	h1 {
		color: #ff3e00;
		text-transform: uppercase;
		font-size: 4em;
		font-weight: 100;
	} 
	table{
		border:1px solid black;
		border-radius: 5px;
		margin:auto;
		width:100%;

	}
	th 
	{
		font-size:1.1em;
	
		padding-top:5px;
		padding-bottom:4px;

	
	}

	* {
		font-family: inherit;
		font-size: inherit;
	}

	input {
		display: block;
		margin: 0 0 0.5em 0;
	}

    .putin input{
		 width:100%;
	}
	.buttons {
		clear: both;
	    
	}


	@media (min-width: 640px) {
		main {
			max-width: none;
		}
	}
</style>
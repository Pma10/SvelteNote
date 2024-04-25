<script>
	let notes = [
		{ id: 1, text: 'TSET' },
	];

	function addNote() {
		const id = notes.length + 1;
		let note_msg = prompt('추가할 노트 내용을 입력하세요 : ');
		notes = [...notes, { id, text: `${note_msg}` }];
	}

	function removeNote(){
		try{
			let num = parseInt(prompt('삭제할 노트 번호를 입력하세요 : '));
			if (isNaN(num)) {
				throw new Error('숫자를 입력해주세요.');
			}
			notes = notes.filter(note => note.id !== num);
		} catch (e) {
			alert("올바른 숫자를 입력해주세요")
		}
	}

	function deleteNote(id) {
		if (confirm("노트를 지우시겠습니까? : ")){
    		notes = notes.filter(note => note.id !== id);
		}
	}
</script>

<svelte:head>
	<title>Notes</title>
	<meta name="description" content="Svelte demo app" />
</svelte:head>

<section>
	<h1>Notes</h1>
	<button on:click={addNote}>+</button>
	<button on:click={removeNote}>-</button>
	{#each notes as note}
		<div class="note-component"><button class="note-button" on:click={deleteNote(note.id)}>{note.id}</button> {note.text}</div>
	{/each}
</section>

<style>
	.note-component {	
		background-color: #f4f4f4;
		padding: 10px;
		margin: 10px 0;
	}
	.note-button {
		background-color: #333;
		color: #fff;
		border: none;
		padding: 5px 10px;
		border-radius: 5px;
		cursor: pointer;
	}
</style>

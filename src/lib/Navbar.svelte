<script>
	let tanggal =''
	const saveTanggal = () => {
		localStorage.setItem('tanggal', tanggal);
		alert('Tanggal berhasil disimpan');
		console.log(localStorage.getItem('tanggal'));
	};
</script>

<nav class="navbar bg-dark navbar-dark fixed-top">
	<div class="container-fluid">
		<a href="/" class="navbar-brand">Pangkalan LPG</a>
		<!-- home -->

		<span class="d-flex">
			<a class="nav-link active" aria-current="page" href="/">Home</a>

			<a class="nav-link" href="/create">Create</a>
		</span>

		<form class="d-flex" role="search">
			<input class="form-control me-2" type="text" placeholder="Input Tanggal" aria-label="text" bind:value={tanggal} />
			<button class="btn btn-outline-success" type="submit" on:click={saveTanggal}>Simpan</button>
		</form>
	</div>
</nav>

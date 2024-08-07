<script>
    export let state;
    export let handleSubmit;
    export let autocomplete;
</script>

<form on:submit|preventDefault={handleSubmit}>
	<div class="mb-1">
		<label for="nik" class="form-label">NIK</label>
		<input
			type="text"
			class="form-control"
			id="nik"
			bind:value={state.nik}
			on:input={autocomplete}
		/>
	</div>
	<div class="mb-1">
		<label for="nama" class="form-label">Nama</label>
		<input type="text" class="form-control" id="nama" bind:value={state.nama} />
	</div>
	<div class="mb-1">
		<label for="alamat" class="form-label">Alamat</label>
		<input type="text" class="form-control" id="alamat" bind:value={state.alamat} />
	</div>
	<div class="mb-1">
		<label for="kategori" class="form-label">Kategori</label>
		<select class="form-select" id="kategori" bind:value={state.kategori}>
			<option value="Rumah Tangga">Rumah Tangga</option>
			<option value="UKM">UKM</option>
		</select>
	</div>
	<div class="mb-1">
		<label for="jtabung" class="form-label">Jumlah Tabung</label>
		<input type="number" class="form-control" id="jtabung" bind:value={state.jtabung} />
	</div>
	<button type="submit" class="btn btn-primary">Submit</button>
	<!-- reset -->
	<button type="reset" class="btn btn-danger">Reset</button>
</form>

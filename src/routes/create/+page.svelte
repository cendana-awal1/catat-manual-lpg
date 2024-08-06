<script>
	import axios from 'axios';
	import data from '../../lib/data.json';
    let apiUrl = import.meta.env.VITE_API_URL

	let state = {
		nik: '',
		nama: '',
		alamat: '',
		kategori: '',
		jtabung: 0,
        tanggal: ''
	};
    $: state.tanggal = localStorage.getItem('tanggal')
    const handleSubmit = async () => {
        console.log(state)
    }
</script>

<h3 class="text-center mt-5">Create</h3>
<div class="container">
	<div class="row justify-content-center">
		<div class="col-md-6">
			<div class="card p-4 mt-1 shadow rounded">
				<form on:submit|preventDefault={handleSubmit}>
					<div class="mb-1">
						<label for="nik" class="form-label">NIK</label>
						<input type="text" class="form-control" id="nik" bind:value={state.nik} />
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
				</form>
			</div>
		</div>
	</div>
</div>
